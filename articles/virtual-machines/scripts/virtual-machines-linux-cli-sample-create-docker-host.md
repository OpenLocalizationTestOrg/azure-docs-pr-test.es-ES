---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear un host Docker | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de un host de Docker"
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="36657-103">Creación de una máquina virtual con Docker</span><span class="sxs-lookup"><span data-stu-id="36657-103">Create a VM with Docker</span></span>

<span data-ttu-id="36657-104">Este script crea una máquina virtual con Docker habilitado e inicia un contenedor de Docker que ejecuta NGINX.</span><span class="sxs-lookup"><span data-stu-id="36657-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="36657-105">Después de ejecutar el script de Hola, puede tener acceso a servidor web de hello NGINX a través de hello FQDN de hello máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="36657-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="36657-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="36657-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="36657-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="36657-107">Clean up deployment</span></span> 

<span data-ttu-id="36657-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="36657-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="36657-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="36657-109">Script explanation</span></span>

<span data-ttu-id="36657-110">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="36657-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="36657-111">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="36657-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="36657-112">Comando</span><span class="sxs-lookup"><span data-stu-id="36657-112">Command</span></span> | <span data-ttu-id="36657-113">Notas</span><span class="sxs-lookup"><span data-stu-id="36657-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="36657-114">az group create</span><span class="sxs-lookup"><span data-stu-id="36657-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="36657-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="36657-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="36657-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="36657-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="36657-117">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="36657-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="36657-118">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="36657-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="36657-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="36657-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="36657-120">Crea un tooallow de regla de grupo de seguridad de red el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="36657-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="36657-121">En este ejemplo, el puerto 80 está abierto al tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="36657-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="36657-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="36657-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="36657-123">Agrega y se ejecuta un tooa de extensión de máquina virtual VM.</span><span class="sxs-lookup"><span data-stu-id="36657-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="36657-124">En este ejemplo, hello extensión de máquina virtual de Docker es tooconfigure usa un host Docker.</span><span class="sxs-lookup"><span data-stu-id="36657-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="36657-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="36657-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="36657-126">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="36657-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36657-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="36657-127">Next steps</span></span>

<span data-ttu-id="36657-128">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36657-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="36657-129">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36657-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
