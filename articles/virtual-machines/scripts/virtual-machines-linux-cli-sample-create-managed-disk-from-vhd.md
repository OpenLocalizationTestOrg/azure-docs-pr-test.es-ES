---
title: "Ejemplo de script de CLI de Azure: creación de un disco administrado a partir de un archivo de disco duro virtual en una cuenta de almacenamiento en la misma suscripción | Microsoft Docs"
description: "Ejemplo de script de CLI de Azure: creación un disco administrado a partir de un archivo de VHD en una cuenta de almacenamiento en la misma suscripción"
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
ms.openlocfilehash: 448636e87db126defc804a613bb61ff19a086ad9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="5f7f8-103">Creación un disco administrado a partir de un archivo de VHD en una cuenta de almacenamiento en la misma suscripción con CLI</span><span class="sxs-lookup"><span data-stu-id="5f7f8-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="5f7f8-104">Este script crea un disco administrado a partir de un archivo de VHD en una cuenta de almacenamiento en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="5f7f8-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="5f7f8-105">Use este script para importar un VHD especializado (no generalizado ni preparado con sysprep) en el disco de sistema operativo administrado para crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5f7f8-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="5f7f8-106">O bien úselo para importar un VHD de datos en el disco de datos administrado.</span><span class="sxs-lookup"><span data-stu-id="5f7f8-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5f7f8-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5f7f8-107">Sample script</span></span>

<span data-ttu-id="5f7f8-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Creación de un disco administrado desde un archivo VHD")]</span><span class="sxs-lookup"><span data-stu-id="5f7f8-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="5f7f8-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5f7f8-109">Script explanation</span></span>

<span data-ttu-id="5f7f8-110">Este script usa los siguientes comandos para crear un disco administrado a partir de un VHD.</span><span class="sxs-lookup"><span data-stu-id="5f7f8-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="5f7f8-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="5f7f8-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5f7f8-112">Comando</span><span class="sxs-lookup"><span data-stu-id="5f7f8-112">Command</span></span> | <span data-ttu-id="5f7f8-113">Notas</span><span class="sxs-lookup"><span data-stu-id="5f7f8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f7f8-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="5f7f8-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="5f7f8-115">Crea un disco administrado usando el identificador URI de un VHD en una cuenta de almacenamiento en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="5f7f8-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f7f8-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f7f8-116">Next steps</span></span>

[<span data-ttu-id="5f7f8-117">Crear una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="5f7f8-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="5f7f8-118">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f7f8-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5f7f8-119">Encontrará más ejemplos de scripts de la CLI de máquina virtual y discos administrados en la [documentación de Azure sobre máquinas virtuales Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f7f8-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
