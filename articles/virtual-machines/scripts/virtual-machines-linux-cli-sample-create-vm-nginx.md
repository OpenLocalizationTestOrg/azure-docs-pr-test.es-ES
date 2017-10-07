---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una VM de Linux con NGINX | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux con NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="88517-103">Creación de una máquina virtual con NGINX</span><span class="sxs-lookup"><span data-stu-id="88517-103">Create a VM with NGINX</span></span>

<span data-ttu-id="88517-104">Este script crea una máquina Virtual de Azure y utiliza Hola extensión de Script personalizado de Azure Virtual Machine tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="88517-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="88517-105">Después de ejecutar el script de Hola, puede tener acceso a un sitio Web de demostración de la dirección IP pública de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="88517-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="88517-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="88517-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="88517-107">Extensión Custom Script</span><span class="sxs-lookup"><span data-stu-id="88517-107">Custom Script Extension</span></span>

<span data-ttu-id="88517-108">extensión de script personalizado de Hello copia esta secuencia de comandos en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="88517-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="88517-109">script de Hola, a continuación, se ejecuta tooinstall y configurar un servidor web NGINX.</span><span class="sxs-lookup"><span data-stu-id="88517-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="88517-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="88517-110">Clean up deployment</span></span> 

<span data-ttu-id="88517-111">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="88517-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="88517-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="88517-112">Script explanation</span></span>

<span data-ttu-id="88517-113">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="88517-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="88517-114">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="88517-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="88517-115">Comando</span><span class="sxs-lookup"><span data-stu-id="88517-115">Command</span></span> | <span data-ttu-id="88517-116">Notas</span><span class="sxs-lookup"><span data-stu-id="88517-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="88517-117">az group create</span><span class="sxs-lookup"><span data-stu-id="88517-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="88517-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="88517-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="88517-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="88517-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="88517-120">Crea la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="88517-120">Creates hello virtual machine.</span></span> <span data-ttu-id="88517-121">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="88517-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="88517-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="88517-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="88517-123">Crea un tooallow de regla de grupo de seguridad de red el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="88517-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="88517-124">En este ejemplo, el puerto 80 está abierto al tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="88517-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="88517-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="88517-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="88517-126">Agrega y se ejecuta un tooa de extensión de máquina virtual VM.</span><span class="sxs-lookup"><span data-stu-id="88517-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="88517-127">En este ejemplo, la extensión de script personalizado de hello es usado tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="88517-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="88517-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="88517-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="88517-129">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="88517-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="88517-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88517-130">Next steps</span></span>

<span data-ttu-id="88517-131">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="88517-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="88517-132">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88517-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
