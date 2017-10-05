---
title: "Ejemplo de script de CLI de Azure: copia (transferencia) de instantánea de un disco administrado en la misma suscripción o en otra con CLI | Microsoft Docs"
description: "Ejemplo de script de CLI de Azure: copia (transferencia) de instantánea de un disco administrado en la misma suscripción o en otra con CLI"
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
ms.openlocfilehash: 6cc0125c08ccb77d014b4642d702c556fffdc8bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="057bd-103">Copia de instantánea de un disco administrado en la misma suscripción o en otra con CLI</span><span class="sxs-lookup"><span data-stu-id="057bd-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="057bd-104">Este script copia una instantánea de un disco administrado en la misma suscripción o en otra.</span><span class="sxs-lookup"><span data-stu-id="057bd-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="057bd-105">Use este script para mover una instantánea a la misma o a otra suscripción en la misma región que la instantánea primaria.</span><span class="sxs-lookup"><span data-stu-id="057bd-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="057bd-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="057bd-106">Sample script</span></span>

<span data-ttu-id="057bd-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copiar instantánea")]</span><span class="sxs-lookup"><span data-stu-id="057bd-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="057bd-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="057bd-108">Script explanation</span></span>

<span data-ttu-id="057bd-109">Este script usa los siguientes comandos para crear una instantánea en la suscripción de destino mediante el identificador de la instantánea de origen.</span><span class="sxs-lookup"><span data-stu-id="057bd-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="057bd-110">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="057bd-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="057bd-111">Comando</span><span class="sxs-lookup"><span data-stu-id="057bd-111">Command</span></span> | <span data-ttu-id="057bd-112">Notas</span><span class="sxs-lookup"><span data-stu-id="057bd-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="057bd-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="057bd-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="057bd-114">Obtiene todas las propiedades de una instantánea usando las propiedades de nombre y grupo de recursos de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="057bd-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="057bd-115">La propiedad del identificador se usa para copiar la instantánea en otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="057bd-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="057bd-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="057bd-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="057bd-117">Copia una instantánea mediante la creación de una instantánea en otra suscripción usando el identificador y nombre de la instantánea primaria.</span><span class="sxs-lookup"><span data-stu-id="057bd-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="057bd-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="057bd-118">Next steps</span></span>

[<span data-ttu-id="057bd-119">Creación de una máquina virtual a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="057bd-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="057bd-120">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="057bd-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="057bd-121">Encontrará más ejemplos de scripts de la CLI de máquina virtual y discos administrados en la [documentación de Azure sobre máquinas virtuales Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="057bd-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
