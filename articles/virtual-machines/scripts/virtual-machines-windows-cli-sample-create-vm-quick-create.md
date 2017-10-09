---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure de creación rápida de una máquina virtual de Windows Server 2016 | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación rápida de una máquina virtual Windows Server 2016"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="1fc8e-103">Creación rápida de una máquina virtual con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1fc8e-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="1fc8e-104">Este script crea una máquina virtual de Azure donde se ejecuta Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="1fc8e-105">Después de ejecutar el script de Hola, puede tener acceso a máquina virtual de Hola a través de una conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1fc8e-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1fc8e-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1fc8e-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="1fc8e-107">Clean up deployment</span></span> 

<span data-ttu-id="1fc8e-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="1fc8e-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="1fc8e-109">Script explanation</span></span>

<span data-ttu-id="1fc8e-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1fc8e-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1fc8e-112">Comando</span><span class="sxs-lookup"><span data-stu-id="1fc8e-112">Command</span></span> | <span data-ttu-id="1fc8e-113">Notas</span><span class="sxs-lookup"><span data-stu-id="1fc8e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1fc8e-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1fc8e-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1fc8e-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1fc8e-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="1fc8e-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1fc8e-117">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="1fc8e-118">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="1fc8e-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="1fc8e-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1fc8e-120">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="1fc8e-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1fc8e-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1fc8e-121">Next steps</span></span>

<span data-ttu-id="1fc8e-122">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1fc8e-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1fc8e-123">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1fc8e-123">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
