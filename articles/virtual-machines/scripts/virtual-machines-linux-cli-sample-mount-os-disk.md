---
title: 'Ejemplo de secuencia de comandos de CLI: el disco del sistema operativo de montaje aaaAzure | Documentos de Microsoft'
description: 'Ejemplo de script de la CLI de Azure: Montaje del disco de sistema operativo'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="971e9-103">Solución de problemas de un disco de sistema operativo de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="971e9-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="971e9-104">Este script monta el disco del sistema operativo Hola de una máquina virtual problemática o con error como datos disco tooa segunda máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="971e9-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="971e9-105">Esto puede ser útil para solucionar problemas de disco o de recuperación de datos.</span><span class="sxs-lookup"><span data-stu-id="971e9-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="971e9-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="971e9-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="971e9-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="971e9-107">Script explanation</span></span>

<span data-ttu-id="971e9-108">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="971e9-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="971e9-109">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="971e9-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="971e9-110">Comando</span><span class="sxs-lookup"><span data-stu-id="971e9-110">Command</span></span> | <span data-ttu-id="971e9-111">Notas</span><span class="sxs-lookup"><span data-stu-id="971e9-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="971e9-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="971e9-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="971e9-113">Devuelve una lista de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="971e9-113">Return a list of virtual machines.</span></span> <span data-ttu-id="971e9-114">En este caso, la opción de consulta de hello es disco del sistema operativo de máquina virtual de tooreturn usado Hola.</span><span class="sxs-lookup"><span data-stu-id="971e9-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="971e9-115">Este valor, a continuación, se agrega el nombre de variable tooa "uri".</span><span class="sxs-lookup"><span data-stu-id="971e9-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="971e9-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="971e9-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="971e9-117">Elimina una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="971e9-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="971e9-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="971e9-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="971e9-119">Crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="971e9-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="971e9-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="971e9-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="971e9-121">Asocia una máquina virtual de tooa de disco.</span><span class="sxs-lookup"><span data-stu-id="971e9-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="971e9-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="971e9-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="971e9-123">Devuelve Hola direcciones IP de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="971e9-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="971e9-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="971e9-124">Next steps</span></span>

<span data-ttu-id="971e9-125">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="971e9-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="971e9-126">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="971e9-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
