---
title: "aaaAzure ejemplo de secuencia de comandos de CLI - copia (movimiento) administrado toosame de discos u otra suscripción | Documentos de Microsoft"
description: "Azure ejemplo de secuencia de comandos CLI - toosame de discos de copia (movimiento) administrado o de otra suscripción"
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
ms.openlocfilehash: b1fa207bd6e05d7094be08855e7823e3b7686013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="9f730-103">Copiar discos administrados toosame u otra suscripción con CLI</span><span class="sxs-lookup"><span data-stu-id="9f730-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="9f730-104">Esta secuencia de comandos copia un disco administrado toosame u otra suscripción pero en Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="9f730-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9f730-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9f730-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="9f730-106">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="9f730-106">Script explanation</span></span>

<span data-ttu-id="9f730-107">Esta secuencia de comandos que se utiliza después de comandos toocreate un nuevo disco administrado en la suscripción de destino de hello con Hola Id. de origen de hello administra el disco.</span><span class="sxs-lookup"><span data-stu-id="9f730-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="9f730-108">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="9f730-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9f730-109">Comando</span><span class="sxs-lookup"><span data-stu-id="9f730-109">Command</span></span> | <span data-ttu-id="9f730-110">Notas</span><span class="sxs-lookup"><span data-stu-id="9f730-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9f730-111">az disk show</span><span class="sxs-lookup"><span data-stu-id="9f730-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="9f730-112">Obtiene todas las propiedades de Hola de un disco administrado mediante propiedades de grupo de hello nombre y los recursos de disco administrado Hola.</span><span class="sxs-lookup"><span data-stu-id="9f730-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="9f730-113">Propiedad ID es toocopy usado Hola administrado disco toodifferent suscripción.</span><span class="sxs-lookup"><span data-stu-id="9f730-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="9f730-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="9f730-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="9f730-115">Copia un disco administrado mediante la creación de un nuevo disco administrado en otra suscripción con el identificador y el nombre primario Hola administrados disco.</span><span class="sxs-lookup"><span data-stu-id="9f730-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="9f730-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f730-116">Next steps</span></span>

[<span data-ttu-id="9f730-117">Crear una máquina virtual a partir de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="9f730-117">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="9f730-118">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9f730-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9f730-119">Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f730-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
