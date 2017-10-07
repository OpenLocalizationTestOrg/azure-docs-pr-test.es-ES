---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure de creación rápida de una VM de Linux | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación rápida de una máquina virtual Linux"
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
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="e94de-103">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e94de-103">Create a virtual machine</span></span>

<span data-ttu-id="e94de-104">Este script crea una máquina virtual de Azure con un sistema operativo Ubuntu y recursos de red relacionados.</span><span class="sxs-lookup"><span data-stu-id="e94de-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="e94de-105">Después de ejecutar el script de Hola, puede tener acceso a máquina virtual de hello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="e94de-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e94de-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e94de-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e94de-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="e94de-107">Clean up deployment</span></span> 

<span data-ttu-id="e94de-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="e94de-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e94de-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="e94de-109">Script explanation</span></span>

<span data-ttu-id="e94de-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e94de-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e94de-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="e94de-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e94de-112">Comando</span><span class="sxs-lookup"><span data-stu-id="e94de-112">Command</span></span> | <span data-ttu-id="e94de-113">Notas</span><span class="sxs-lookup"><span data-stu-id="e94de-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e94de-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e94de-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e94de-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="e94de-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e94de-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="e94de-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e94de-117">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="e94de-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="e94de-118">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="e94de-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="e94de-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="e94de-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e94de-120">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="e94de-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e94de-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e94de-121">Next steps</span></span>

<span data-ttu-id="e94de-122">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e94de-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e94de-123">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e94de-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
