---
title: "Ejemplo de script de la CLI de Azure: creación de un host de Docker | Microsoft Docs"
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
ms.openlocfilehash: e8704824dec66d724f2d30dab4d6bdf019c6b206
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="5d8c8-103">Creación de una máquina virtual con Docker</span><span class="sxs-lookup"><span data-stu-id="5d8c8-103">Create a VM with Docker</span></span>

<span data-ttu-id="5d8c8-104">Este script crea una máquina virtual con Docker habilitado e inicia un contenedor de Docker que ejecuta NGINX.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="5d8c8-105">Una vez que el script se ha ejecutado, puede acceder al servidor web NGINX es accesible mediante el FQDN de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5d8c8-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5d8c8-106">Sample script</span></span>

<span data-ttu-id="5d8c8-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Host de Docker")]</span><span class="sxs-lookup"><span data-stu-id="5d8c8-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5d8c8-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5d8c8-108">Clean up deployment</span></span> 

<span data-ttu-id="5d8c8-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5d8c8-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5d8c8-110">Script explanation</span></span>

<span data-ttu-id="5d8c8-111">Este script usa los siguientes comandos para crear la implementación.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5d8c8-112">Cada elemento de la tabla incluye vínculos a la documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5d8c8-113">Comando</span><span class="sxs-lookup"><span data-stu-id="5d8c8-113">Command</span></span> | <span data-ttu-id="5d8c8-114">Notas</span><span class="sxs-lookup"><span data-stu-id="5d8c8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d8c8-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5d8c8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5d8c8-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5d8c8-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="5d8c8-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5d8c8-118">Crea la máquina virtual y la conecta con la tarjeta de red, la red virtual, la subred y el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="5d8c8-119">Este comando también especifica la imagen de máquina virtual que se usará, y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="5d8c8-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="5d8c8-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="5d8c8-121">Crea una regla de grupo de seguridad de red para permitir el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="5d8c8-122">En este ejemplo, el puerto 80 está abierto al tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="5d8c8-123">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="5d8c8-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5d8c8-124">Agrega una extensión de máquina virtual a una máquina virtual y la ejecuta.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="5d8c8-125">En este ejemplo, se usa la extensión de máquina virtual de Docker para configurar un host de Docker.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-125">In this sample, the Docker VM extension is used to configure a Docker host.</span></span>|
| [<span data-ttu-id="5d8c8-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="5d8c8-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5d8c8-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="5d8c8-127">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d8c8-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d8c8-128">Next steps</span></span>

<span data-ttu-id="5d8c8-129">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d8c8-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5d8c8-130">Encontrará más ejemplos de scripts de la CLI de máquina virtual en la [documentación sobre máquinas virtuales Linux de Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d8c8-130">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
