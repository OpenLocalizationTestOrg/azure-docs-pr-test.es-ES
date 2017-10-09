---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una máquina virtual de Windows Server 2016 con la supervisión de OMS | Documentos de Microsoft"
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
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="d9f35-103">Supervisión de una máquina virtual con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="d9f35-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="d9f35-104">Este script crea una máquina Virtual de Azure, instala al agente de Operations Management Suite (OMS) hello e inscribe sistema Hola con un área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="d9f35-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="d9f35-105">Una vez que se ejecutó la secuencia de comandos de hello, máquina virtual de hello serán visible en la consola de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="d9f35-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d9f35-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d9f35-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d9f35-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="d9f35-107">Clean up deployment</span></span> 

<span data-ttu-id="d9f35-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="d9f35-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d9f35-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d9f35-109">Script explanation</span></span>

<span data-ttu-id="d9f35-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d9f35-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d9f35-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="d9f35-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d9f35-112">Comando</span><span class="sxs-lookup"><span data-stu-id="d9f35-112">Command</span></span> | <span data-ttu-id="d9f35-113">Notas</span><span class="sxs-lookup"><span data-stu-id="d9f35-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d9f35-114">az group create</span><span class="sxs-lookup"><span data-stu-id="d9f35-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d9f35-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d9f35-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d9f35-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="d9f35-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d9f35-117">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="d9f35-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="d9f35-118">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="d9f35-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="d9f35-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="d9f35-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d9f35-120">Ejecuta una extensión de máquina virtual en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9f35-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="d9f35-121">En este caso, Hola extensión del agente Operations Management Suite tooinstall usado Hola OMS agente e inscribir Hola máquina virtual en un área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="d9f35-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="d9f35-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="d9f35-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d9f35-123">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="d9f35-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d9f35-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9f35-124">Next steps</span></span>

<span data-ttu-id="d9f35-125">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d9f35-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d9f35-126">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d9f35-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
