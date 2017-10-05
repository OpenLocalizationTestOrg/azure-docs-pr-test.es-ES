---
title: "Ejemplo de script de la CLI de Azure: creación rápida de una máquina virtual Windows Server 2016 | Microsoft Docs"
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
ms.openlocfilehash: 084518bf7bc1d01c4a146efe3e0b7fe08149ce35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="0e087-103">Creación rápida de una máquina virtual con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0e087-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="0e087-104">Este script crea una máquina virtual de Azure donde se ejecuta Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0e087-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="0e087-105">Después de ejecutar el script, puede acceder a la máquina virtual a través de una conexión al Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="0e087-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0e087-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0e087-106">Sample script</span></span>

<span data-ttu-id="0e087-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Creación rápida de una máquina virtual")]</span><span class="sxs-lookup"><span data-stu-id="0e087-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0e087-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="0e087-108">Clean up deployment</span></span> 

<span data-ttu-id="0e087-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0e087-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="0e087-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0e087-110">Script explanation</span></span>

<span data-ttu-id="0e087-111">Este script usa los siguientes comandos para crear un grupo de recursos, una máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0e087-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="0e087-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="0e087-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0e087-113">Comando</span><span class="sxs-lookup"><span data-stu-id="0e087-113">Command</span></span> | <span data-ttu-id="0e087-114">Notas</span><span class="sxs-lookup"><span data-stu-id="0e087-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0e087-115">az group create</span><span class="sxs-lookup"><span data-stu-id="0e087-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0e087-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0e087-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0e087-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="0e087-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="0e087-118">Crea la máquina virtual y la conecta con la tarjeta de red, la red virtual, la subred y el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="0e087-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="0e087-119">Este comando también especifica la imagen de máquina virtual que se usará, y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="0e087-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="0e087-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="0e087-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0e087-121">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="0e087-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0e087-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e087-122">Next steps</span></span>

<span data-ttu-id="0e087-123">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0e087-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0e087-124">Encontrará más ejemplos de scripts de la CLI de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e087-124">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
