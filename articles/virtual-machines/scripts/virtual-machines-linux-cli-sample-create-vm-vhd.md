---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una máquina virtual con un disco duro virtual | Documentos de Microsoft"
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
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="68884-103">Crear una máquina virtual con un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="68884-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="68884-104">Este ejemplo crea una máquina virtual con un disco duro virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="68884-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="68884-105">Crea un grupo de recursos, una cuenta de almacenamiento y un contenedor, a continuación, crea una máquina virtual mediante la carga de contenedor de hello VHD toohello.</span><span class="sxs-lookup"><span data-stu-id="68884-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="68884-106">Reemplaza Hola ssh público de clave con la clave pública para que tenga acceso toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68884-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="68884-107">Necesitará un VHD de arranque.</span><span class="sxs-lookup"><span data-stu-id="68884-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="68884-108">Puede descargar Hola VHD que hemos usado desde https://azclisamples.blob.core.windows.net/vhds/sample.vhd o usar un VHD propio.</span><span class="sxs-lookup"><span data-stu-id="68884-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="68884-109">busca el script de Hola `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="68884-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="68884-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="68884-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="68884-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="68884-111">Clean up deployment</span></span> 

<span data-ttu-id="68884-112">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="68884-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="68884-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="68884-113">Script explanation</span></span>

<span data-ttu-id="68884-114">Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="68884-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="68884-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="68884-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="68884-116">Comando</span><span class="sxs-lookup"><span data-stu-id="68884-116">Command</span></span> | <span data-ttu-id="68884-117">Notas</span><span class="sxs-lookup"><span data-stu-id="68884-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="68884-118">az group create</span><span class="sxs-lookup"><span data-stu-id="68884-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="68884-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="68884-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="68884-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="68884-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="68884-121">Enumera las cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="68884-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="68884-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="68884-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="68884-123">Comprueba que un nombre de cuenta de almacenamiento es válido y que no existe ya</span><span class="sxs-lookup"><span data-stu-id="68884-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="68884-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="68884-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="68884-125">Enumera las claves hello las cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="68884-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="68884-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="68884-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="68884-127">Comprueba si existe el blob de Hola</span><span class="sxs-lookup"><span data-stu-id="68884-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="68884-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="68884-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="68884-129">Crea un contenedor en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="68884-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="68884-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="68884-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="68884-131">Crea un blob en contenedor Hola Hola cargar VHD.</span><span class="sxs-lookup"><span data-stu-id="68884-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="68884-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="68884-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="68884-133">Usar con `--query` comprobar si el nombre de la máquina virtual de hello está en uso.</span><span class="sxs-lookup"><span data-stu-id="68884-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="68884-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="68884-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="68884-135">Crea hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="68884-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="68884-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="68884-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="68884-137">Restablece Hola SSH toogive clave Hola actual usuario acceso toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68884-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="68884-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="68884-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="68884-139">Obtiene la dirección IP de Hola de hello máquina virtual que se creó.</span><span class="sxs-lookup"><span data-stu-id="68884-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68884-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68884-140">Next steps</span></span>

<span data-ttu-id="68884-141">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="68884-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="68884-142">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68884-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
