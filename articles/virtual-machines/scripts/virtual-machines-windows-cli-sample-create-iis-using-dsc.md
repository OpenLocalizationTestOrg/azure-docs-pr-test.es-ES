---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una VM de Windows Server 2016 con IIS mediante DSC | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Windows Server 2016 con IIS mediante DSC"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="e72a4-103">Creación de una máquina virtual con IIS mediante DSC</span><span class="sxs-lookup"><span data-stu-id="e72a4-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="e72a4-104">Este script crea una máquina virtual y utiliza tooinstall de extensión de script personalizado de DSC de máquina Virtual de Azure de Hola y configura IIS.</span><span class="sxs-lookup"><span data-stu-id="e72a4-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e72a4-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e72a4-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e72a4-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="e72a4-106">Clean up deployment</span></span> 

<span data-ttu-id="e72a4-107">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="e72a4-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e72a4-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="e72a4-108">Script explanation</span></span>

<span data-ttu-id="e72a4-109">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e72a4-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e72a4-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="e72a4-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e72a4-111">Comando</span><span class="sxs-lookup"><span data-stu-id="e72a4-111">Command</span></span> | <span data-ttu-id="e72a4-112">Notas</span><span class="sxs-lookup"><span data-stu-id="e72a4-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e72a4-113">az group create</span><span class="sxs-lookup"><span data-stu-id="e72a4-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e72a4-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="e72a4-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e72a4-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="e72a4-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e72a4-116">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="e72a4-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="e72a4-117">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="e72a4-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="e72a4-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="e72a4-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e72a4-119">Agregar máquina virtual de toohello de extensión de Script personalizado de Hola que invoca un tooinstall script IIS.</span><span class="sxs-lookup"><span data-stu-id="e72a4-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="e72a4-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="e72a4-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="e72a4-121">Crea un tooallow de regla de grupo de seguridad de red el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="e72a4-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="e72a4-122">En este ejemplo, el puerto 80 está abierto al tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="e72a4-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="e72a4-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="e72a4-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e72a4-124">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="e72a4-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e72a4-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e72a4-125">Next steps</span></span>

<span data-ttu-id="e72a4-126">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e72a4-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e72a4-127">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e72a4-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
