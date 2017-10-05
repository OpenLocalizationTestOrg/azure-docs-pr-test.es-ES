---
title: "Ejemplo de script de la CLI de Azure: crear una máquina virtual con un disco duro virtual | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: crear una máquina virtual mediante un disco duro virtual."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: fab65296a552c1839522c5254a868a3dc96227f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="f5a78-103">Crear una máquina virtual con un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="f5a78-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="f5a78-104">Este ejemplo crea una máquina virtual con un disco duro virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="f5a78-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="f5a78-105">Crea un grupo de recursos, una cuenta de almacenamiento y un contenedor, y después carga el VHD en el contenedor para crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f5a78-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="f5a78-106">Reemplaza la clave pública SSH con su clave pública para que tenga acceso a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f5a78-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="f5a78-107">Necesitará un VHD de arranque.</span><span class="sxs-lookup"><span data-stu-id="f5a78-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="f5a78-108">Puede usar su propio VHD o descargar el que hemos usado desde https://azclisamples.blob.core.windows.net/vhds/sample.vhd.</span><span class="sxs-lookup"><span data-stu-id="f5a78-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="f5a78-109">El script busca `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="f5a78-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f5a78-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f5a78-110">Sample script</span></span>

<span data-ttu-id="f5a78-111">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Crear máquina virtual con un disco duro virtual")]</span><span class="sxs-lookup"><span data-stu-id="f5a78-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f5a78-112">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="f5a78-112">Clean up deployment</span></span> 

<span data-ttu-id="f5a78-113">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f5a78-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="f5a78-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f5a78-114">Script explanation</span></span>

<span data-ttu-id="f5a78-115">Este script usa los siguientes comandos para crear un grupo de recursos, una máquina virtual, un conjunto de disponibilidad, un equilibrador de carga y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f5a78-115">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="f5a78-116">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="f5a78-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f5a78-117">Comando</span><span class="sxs-lookup"><span data-stu-id="f5a78-117">Command</span></span> | <span data-ttu-id="f5a78-118">Notas</span><span class="sxs-lookup"><span data-stu-id="f5a78-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f5a78-119">az group create</span><span class="sxs-lookup"><span data-stu-id="f5a78-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f5a78-120">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f5a78-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f5a78-121">az storage account list</span><span class="sxs-lookup"><span data-stu-id="f5a78-121">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="f5a78-122">Enumera las cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f5a78-122">Lists storage accounts</span></span> |
| [<span data-ttu-id="f5a78-123">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="f5a78-123">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="f5a78-124">Comprueba que un nombre de cuenta de almacenamiento es válido y que no existe ya</span><span class="sxs-lookup"><span data-stu-id="f5a78-124">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="f5a78-125">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="f5a78-125">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="f5a78-126">Enumera las claves de las cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f5a78-126">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="f5a78-127">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="f5a78-127">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="f5a78-128">Comprueba si existe el blob</span><span class="sxs-lookup"><span data-stu-id="f5a78-128">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="f5a78-129">az storage container create</span><span class="sxs-lookup"><span data-stu-id="f5a78-129">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="f5a78-130">Crea un contenedor en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f5a78-130">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="f5a78-131">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="f5a78-131">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="f5a78-132">Crea un blob en el contenedor cargando el VHD.</span><span class="sxs-lookup"><span data-stu-id="f5a78-132">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="f5a78-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="f5a78-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="f5a78-134">Se usa con `--query` para comprobar si el nombre de la máquina virtual está en uso.</span><span class="sxs-lookup"><span data-stu-id="f5a78-134">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="f5a78-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="f5a78-135">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="f5a78-136">Crea las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f5a78-136">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="f5a78-137">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="f5a78-137">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="f5a78-138">Restablece la clave SSH para permitir el acceso del usuario actual a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f5a78-138">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="f5a78-139">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="f5a78-139">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="f5a78-140">Obtiene la dirección IP de la máquina virtual que se creó.</span><span class="sxs-lookup"><span data-stu-id="f5a78-140">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f5a78-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5a78-141">Next steps</span></span>

<span data-ttu-id="f5a78-142">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5a78-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f5a78-143">Encontrará más ejemplos de scripts de la CLI de máquina virtual en la [documentación sobre máquinas virtuales Linux de Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f5a78-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
