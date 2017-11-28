---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear dos máquinas virtuales con un NSG interno y externo | Documentos de Microsoft"
description: "Ejemplo de script de CLI de Azure: creación de dos máquinas virtuales con un NSG interno y externo"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="2433d-103">Protección del tráfico de red entre máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="2433d-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="2433d-104">Esta secuencia de comandos crea dos máquinas virtuales y protege el tooboth de tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="2433d-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="2433d-105">Una máquina virtual es accesible en internet de Hola y ha configurado un grupo de seguridad de red (NSG) tooallow tráfico en el puerto 80 y el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="2433d-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="2433d-106">Hola segundo una máquina virtual no es accesible en Hola internet y ha un tooonly NSG configurado que permita el tráfico de la máquina virtual de primera Hola.</span><span class="sxs-lookup"><span data-stu-id="2433d-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2433d-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2433d-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2433d-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="2433d-108">Clean up deployment</span></span> 

<span data-ttu-id="2433d-109">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="2433d-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2433d-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2433d-110">Script explanation</span></span>

<span data-ttu-id="2433d-111">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2433d-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2433d-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="2433d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2433d-113">Comando</span><span class="sxs-lookup"><span data-stu-id="2433d-113">Command</span></span> | <span data-ttu-id="2433d-114">Notas</span><span class="sxs-lookup"><span data-stu-id="2433d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2433d-115">az group create</span><span class="sxs-lookup"><span data-stu-id="2433d-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2433d-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="2433d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2433d-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="2433d-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="2433d-118">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="2433d-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="2433d-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="2433d-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="2433d-120">Crea una subred.</span><span class="sxs-lookup"><span data-stu-id="2433d-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="2433d-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="2433d-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2433d-122">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="2433d-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="2433d-123">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="2433d-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="2433d-124">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="2433d-124">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="2433d-125">Actualiza una regla de NSG.</span><span class="sxs-lookup"><span data-stu-id="2433d-125">Updates an NSG rule.</span></span> <span data-ttu-id="2433d-126">En este ejemplo, la regla de back-end de hello es toopass actualizados por el tráfico sólo de subred de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2433d-126">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="2433d-127">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="2433d-127">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="2433d-128">Devuelve información acerca de una regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="2433d-128">Returns information about a network security group rule.</span></span> <span data-ttu-id="2433d-129">En este ejemplo, el nombre de la regla de Hola se almacena en una variable para usarlo más adelante en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="2433d-129">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="2433d-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="2433d-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2433d-131">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="2433d-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2433d-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2433d-132">Next steps</span></span>

<span data-ttu-id="2433d-133">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2433d-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2433d-134">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2433d-134">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
