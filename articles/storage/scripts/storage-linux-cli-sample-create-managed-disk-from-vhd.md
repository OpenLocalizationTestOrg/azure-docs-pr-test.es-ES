---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en hello misma suscripción | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en hello misma suscripción"
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
ms.openlocfilehash: 1e792fdbb7daea92bf6a6589a5d8aab5b9b5a670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="2644b-103">Crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento de hello misma suscripción con CLI</span><span class="sxs-lookup"><span data-stu-id="2644b-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="2644b-104">Este script crea un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="2644b-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="2644b-105">Utilice este tooimport script un versión especializada del toocreate de (no generalizado/preparada con Sysprep) VHD toomanaged OS disco una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2644b-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="2644b-106">O bien, use un disco de datos de datos VHD toomanaged tooimport.</span><span class="sxs-lookup"><span data-stu-id="2644b-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2644b-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2644b-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="2644b-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2644b-108">Script explanation</span></span>

<span data-ttu-id="2644b-109">Este script usará los siguientes comandos toocreate un disco administrado desde un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="2644b-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="2644b-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="2644b-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2644b-111">Comando</span><span class="sxs-lookup"><span data-stu-id="2644b-111">Command</span></span> | <span data-ttu-id="2644b-112">Notas</span><span class="sxs-lookup"><span data-stu-id="2644b-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2644b-113">az disk create</span><span class="sxs-lookup"><span data-stu-id="2644b-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="2644b-114">Crea un disco administrado usando el identificador URI de un disco duro virtual en una cuenta de almacenamiento de hello misma suscripción</span><span class="sxs-lookup"><span data-stu-id="2644b-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2644b-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2644b-115">Next steps</span></span>

[<span data-ttu-id="2644b-116">Creación de una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="2644b-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="2644b-117">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2644b-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2644b-118">Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2644b-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
