---
title: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux | Microsoft Docs"
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
ms.openlocfilehash: dc7e7276bcea32c59c67a42dedaffcedfd0cf907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="02614-103">Creación una máquina virtual completamente configurada</span><span class="sxs-lookup"><span data-stu-id="02614-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="02614-104">Este script crea una máquina virtual de Azure con un sistema operativo Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="02614-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="02614-105">Después de ejecutar el script, puede acceder a la máquina virtual a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="02614-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="02614-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="02614-106">Sample script</span></span>

<span data-ttu-id="02614-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Creación rápida de una máquina virtual")]</span><span class="sxs-lookup"><span data-stu-id="02614-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="02614-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="02614-108">Clean up deployment</span></span> 

<span data-ttu-id="02614-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="02614-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="02614-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="02614-110">Script explanation</span></span>

<span data-ttu-id="02614-111">Este script usa los siguientes comandos para crear un grupo de recursos, una máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="02614-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="02614-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="02614-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="02614-113">Comando</span><span class="sxs-lookup"><span data-stu-id="02614-113">Command</span></span> | <span data-ttu-id="02614-114">Notas</span><span class="sxs-lookup"><span data-stu-id="02614-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="02614-115">az group create</span><span class="sxs-lookup"><span data-stu-id="02614-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="02614-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="02614-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="02614-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="02614-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="02614-118">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="02614-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="02614-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="02614-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="02614-120">Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado.</span><span class="sxs-lookup"><span data-stu-id="02614-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="02614-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="02614-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="02614-122">Crea un grupo de seguridad de red (NSG), que es un límite de seguridad entre Internet y la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02614-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="02614-123">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="02614-123">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="02614-124">Crea una regla de NSG para permitir el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="02614-124">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="02614-125">En este ejemplo, el puerto 22 está abierto al tráfico SSH.</span><span class="sxs-lookup"><span data-stu-id="02614-125">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="02614-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="02614-126">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="02614-127">Crea una tarjeta de máquina virtual y la conecta con la red virtual, la subred y el NSG.</span><span class="sxs-lookup"><span data-stu-id="02614-127">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="02614-128">az vm create</span><span class="sxs-lookup"><span data-stu-id="02614-128">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="02614-129">Crea la máquina virtual y la conecta con la tarjeta de red, la red virtual, la subred y el NSG.</span><span class="sxs-lookup"><span data-stu-id="02614-129">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="02614-130">Este comando también especifica la imagen de máquina virtual que se usará, y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="02614-130">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="02614-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="02614-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="02614-132">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="02614-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="02614-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02614-133">Next steps</span></span>

<span data-ttu-id="02614-134">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="02614-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="02614-135">Encontrará más ejemplos de scripts de la CLI de máquina virtual en la [documentación sobre máquinas virtuales Linux de Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02614-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
