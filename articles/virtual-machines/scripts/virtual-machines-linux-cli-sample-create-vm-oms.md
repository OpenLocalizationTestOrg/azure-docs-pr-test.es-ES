---
title: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux con supervisión de OMS | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux con supervisión de OMS"
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
ms.openlocfilehash: 31bfcc532a7d1ea418fb9a15ec882963d1913756
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="2072a-103">Supervisión de una máquina virtual con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="2072a-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="2072a-104">Este script crea una máquina virtual de Azure, instala el agente de Operations Management Suite (OMS) e inscribe el sistema en un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="2072a-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="2072a-105">Después de ejecutar el script, la máquina virtual será visible en la consola de OMS.</span><span class="sxs-lookup"><span data-stu-id="2072a-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2072a-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2072a-106">Sample script</span></span>

<span data-ttu-id="2072a-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Creación rápida de una máquina virtual")]</span><span class="sxs-lookup"><span data-stu-id="2072a-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2072a-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="2072a-108">Clean up deployment</span></span> 

<span data-ttu-id="2072a-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2072a-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2072a-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2072a-110">Script explanation</span></span>

<span data-ttu-id="2072a-111">Este script usa los siguientes comandos para crear un grupo de recursos, una máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2072a-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2072a-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="2072a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2072a-113">Comando</span><span class="sxs-lookup"><span data-stu-id="2072a-113">Command</span></span> | <span data-ttu-id="2072a-114">Notas</span><span class="sxs-lookup"><span data-stu-id="2072a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2072a-115">az group create</span><span class="sxs-lookup"><span data-stu-id="2072a-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2072a-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="2072a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2072a-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="2072a-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2072a-118">Crea la máquina virtual y la conecta con la tarjeta de red, la red virtual, la subred y el NSG.</span><span class="sxs-lookup"><span data-stu-id="2072a-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="2072a-119">Este comando también especifica la imagen de máquina virtual que se usará, y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="2072a-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="2072a-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="2072a-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2072a-121">Ejecuta una extensión de máquina virtual en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2072a-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="2072a-122">En este caso, la extensión de agente de Operations Management Suite se usa para instalar el agente de OMS e inscribir la máquina virtual en un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="2072a-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="2072a-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="2072a-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2072a-124">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="2072a-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2072a-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2072a-125">Next steps</span></span>

<span data-ttu-id="2072a-126">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2072a-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2072a-127">Encontrará más ejemplos de scripts de la CLI de máquina virtual en la [documentación sobre máquinas virtuales Linux de Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2072a-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
