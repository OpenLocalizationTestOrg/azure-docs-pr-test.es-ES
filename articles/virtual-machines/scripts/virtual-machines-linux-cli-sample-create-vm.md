---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una VM de Linux | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux"
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
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="baab7-103">Creación una máquina virtual completamente configurada</span><span class="sxs-lookup"><span data-stu-id="baab7-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="baab7-104">Este script crea una máquina virtual de Azure con un sistema operativo Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="baab7-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="baab7-105">Después de ejecutar el script de Hola, puede tener acceso a máquina virtual de hello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="baab7-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="baab7-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="baab7-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="baab7-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="baab7-107">Clean up deployment</span></span> 

<span data-ttu-id="baab7-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="baab7-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="baab7-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="baab7-109">Script explanation</span></span>

<span data-ttu-id="baab7-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="baab7-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="baab7-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="baab7-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="baab7-112">Comando</span><span class="sxs-lookup"><span data-stu-id="baab7-112">Command</span></span> | <span data-ttu-id="baab7-113">Notas</span><span class="sxs-lookup"><span data-stu-id="baab7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="baab7-114">az group create</span><span class="sxs-lookup"><span data-stu-id="baab7-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="baab7-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="baab7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="baab7-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="baab7-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="baab7-117">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="baab7-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="baab7-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="baab7-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="baab7-119">Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado.</span><span class="sxs-lookup"><span data-stu-id="baab7-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="baab7-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="baab7-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="baab7-121">Crea un grupo de seguridad de red (NSG), que es un límite de seguridad entre Hola internet y hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="baab7-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="baab7-122">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="baab7-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="baab7-123">Crea un tooallow de regla NSG el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="baab7-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="baab7-124">En este ejemplo, el puerto 22 está abierto al tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="baab7-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="baab7-125">az network nic create</span><span class="sxs-lookup"><span data-stu-id="baab7-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="baab7-126">Crea una tarjeta de red virtual y lo adjunta toohello de red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="baab7-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="baab7-127">az vm create</span><span class="sxs-lookup"><span data-stu-id="baab7-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="baab7-128">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="baab7-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="baab7-129">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="baab7-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="baab7-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="baab7-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="baab7-131">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="baab7-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="baab7-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="baab7-132">Next steps</span></span>

<span data-ttu-id="baab7-133">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="baab7-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="baab7-134">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="baab7-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
