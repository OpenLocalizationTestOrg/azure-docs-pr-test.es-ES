---
title: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Windows Server 2016 con supervisión de OMS | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Windows Server 2016 con supervisión de OMS"
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
ms.author: rclaus
ms.openlocfilehash: ddb191163061dc47712e024c8c1d7a6f4bdf325b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="6d900-103">Supervisión de una máquina virtual con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6d900-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="6d900-104">Este script crea una máquina virtual de Azure, instala el agente de Operations Management Suite (OMS) e inscribe el sistema en un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6d900-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="6d900-105">Después de ejecutar el script, la máquina virtual será visible en la consola de OMS.</span><span class="sxs-lookup"><span data-stu-id="6d900-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6d900-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d900-106">Sample script</span></span>

<span data-ttu-id="6d900-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Creación rápida de una máquina virtual")]</span><span class="sxs-lookup"><span data-stu-id="6d900-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6d900-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="6d900-108">Clean up deployment</span></span> 

<span data-ttu-id="6d900-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6d900-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6d900-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6d900-110">Script explanation</span></span>

<span data-ttu-id="6d900-111">Este script usa los siguientes comandos para crear un grupo de recursos, una máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6d900-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6d900-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="6d900-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6d900-113">Comando</span><span class="sxs-lookup"><span data-stu-id="6d900-113">Command</span></span> | <span data-ttu-id="6d900-114">Notas</span><span class="sxs-lookup"><span data-stu-id="6d900-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d900-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6d900-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6d900-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6d900-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d900-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="6d900-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6d900-118">Crea la máquina virtual y la conecta con la tarjeta de red, la red virtual, la subred y el NSG.</span><span class="sxs-lookup"><span data-stu-id="6d900-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6d900-119">Este comando también especifica la imagen de máquina virtual que se usará, y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="6d900-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="6d900-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="6d900-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6d900-121">Ejecuta una extensión de máquina virtual en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d900-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="6d900-122">En este caso, la extensión de agente de Operations Management Suite se usa para instalar el agente de OMS e inscribir la máquina virtual en un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6d900-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="6d900-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="6d900-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6d900-124">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="6d900-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d900-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d900-125">Next steps</span></span>

<span data-ttu-id="6d900-126">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d900-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d900-127">Encontrará más ejemplos de scripts de la CLI de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d900-127">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
