---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una VM de Windows Server | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Windows Server"
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
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="5c9de-103">Crear una máquina virtual con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5c9de-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="5c9de-104">Este script crea una máquina virtual de Azure donde se ejecuta Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5c9de-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="5c9de-105">Después de ejecutar el script de Hola, puede tener acceso a máquina virtual de Hola a través de una conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="5c9de-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c9de-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5c9de-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5c9de-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5c9de-107">Clean up deployment</span></span> 

<span data-ttu-id="5c9de-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="5c9de-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5c9de-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5c9de-109">Script explanation</span></span>

<span data-ttu-id="5c9de-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5c9de-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5c9de-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="5c9de-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5c9de-112">Comando</span><span class="sxs-lookup"><span data-stu-id="5c9de-112">Command</span></span> | <span data-ttu-id="5c9de-113">Notas</span><span class="sxs-lookup"><span data-stu-id="5c9de-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c9de-114">az group create</span><span class="sxs-lookup"><span data-stu-id="5c9de-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5c9de-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="5c9de-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5c9de-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="5c9de-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="5c9de-117">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9de-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="5c9de-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="5c9de-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="5c9de-119">Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado.</span><span class="sxs-lookup"><span data-stu-id="5c9de-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="5c9de-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="5c9de-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="5c9de-121">Crea un grupo de seguridad de red (NSG), que es un límite de seguridad entre Hola internet y hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5c9de-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="5c9de-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="5c9de-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="5c9de-123">Crea una tarjeta de red virtual y lo adjunta toohello de red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="5c9de-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="5c9de-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="5c9de-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5c9de-125">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="5c9de-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="5c9de-126">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="5c9de-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="5c9de-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="5c9de-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5c9de-128">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="5c9de-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c9de-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c9de-129">Next steps</span></span>

<span data-ttu-id="5c9de-130">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c9de-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5c9de-131">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c9de-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
