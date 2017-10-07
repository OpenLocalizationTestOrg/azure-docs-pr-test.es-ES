---
title: "Ejemplo de secuencia de comandos de CLI: instantánea de copia (movimiento) de un disco administrado toosame u otra suscripción con CLI aaaAzure | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - instantánea de copia (movimiento) de un disco administrado toosame u otra suscripción con CLI"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="5b6a3-103">Instantánea de copia de un disco administrado toosame o de otra suscripción con CLI</span><span class="sxs-lookup"><span data-stu-id="5b6a3-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="5b6a3-104">Este script copia una instantánea de un disco administrado toosame o suscripción diferente.</span><span class="sxs-lookup"><span data-stu-id="5b6a3-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="5b6a3-105">Utilice este toomove script una suscripción de instantánea toodifferent Hola misma región que la instantánea primaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b6a3-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5b6a3-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b6a3-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="5b6a3-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5b6a3-107">Script explanation</span></span>

<span data-ttu-id="5b6a3-108">Este script utiliza después comandos toocreate una instantánea en la suscripción de destino de hello con Hola Id. de instantánea de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="5b6a3-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="5b6a3-109">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="5b6a3-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5b6a3-110">Comando</span><span class="sxs-lookup"><span data-stu-id="5b6a3-110">Command</span></span> | <span data-ttu-id="5b6a3-111">Notas</span><span class="sxs-lookup"><span data-stu-id="5b6a3-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5b6a3-112">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="5b6a3-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="5b6a3-113">Obtiene todas las propiedades de Hola de una instantánea mediante el nombre de Hola y propiedades de grupo de recursos de instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b6a3-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="5b6a3-114">Propiedad ID es toocopy usado Hola instantánea toodifferent suscripción.</span><span class="sxs-lookup"><span data-stu-id="5b6a3-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="5b6a3-115">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="5b6a3-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="5b6a3-116">Copia una instantánea mediante la creación de una instantánea de sesión con otra suscripción Hola identificador y el nombre de Hola instantánea primaria.</span><span class="sxs-lookup"><span data-stu-id="5b6a3-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="5b6a3-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b6a3-117">Next steps</span></span>

[<span data-ttu-id="5b6a3-118">Crear una máquina virtual a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="5b6a3-118">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="5b6a3-119">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5b6a3-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5b6a3-120">Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b6a3-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
