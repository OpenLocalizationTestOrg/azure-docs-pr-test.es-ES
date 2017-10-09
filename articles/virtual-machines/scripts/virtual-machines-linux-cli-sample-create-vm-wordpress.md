---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una VM de Linux con WordPress | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual Linux con WordPress"
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
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="24eaf-103">Creación de una máquina virtual con WordPress</span><span class="sxs-lookup"><span data-stu-id="24eaf-103">Create a VM with WordPress</span></span>

<span data-ttu-id="24eaf-104">Este script crea una máquina virtual y, a continuación, usa un script personalizado extensión tooinstall WordPress de hello Máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="24eaf-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="24eaf-105">Después de ejecutar script de Hola, puede tener acceso a sitio de configuración de WordPress hello en `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="24eaf-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="24eaf-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="24eaf-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="24eaf-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="24eaf-107">Clean up deployment</span></span> 

<span data-ttu-id="24eaf-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="24eaf-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="24eaf-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="24eaf-109">Script explanation</span></span>

<span data-ttu-id="24eaf-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="24eaf-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="24eaf-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="24eaf-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="24eaf-112">Comando</span><span class="sxs-lookup"><span data-stu-id="24eaf-112">Command</span></span> | <span data-ttu-id="24eaf-113">Notas</span><span class="sxs-lookup"><span data-stu-id="24eaf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24eaf-114">az group create</span><span class="sxs-lookup"><span data-stu-id="24eaf-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="24eaf-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="24eaf-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="24eaf-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="24eaf-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="24eaf-117">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG.</span><span class="sxs-lookup"><span data-stu-id="24eaf-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="24eaf-118">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="24eaf-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="24eaf-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="24eaf-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="24eaf-120">Crea un tooallow de regla de grupo de seguridad de red el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="24eaf-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="24eaf-121">En este ejemplo, el puerto 80 está abierto al tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="24eaf-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="24eaf-122">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="24eaf-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="24eaf-123">Agregar máquina virtual de hello extensión de Script personalizado toohello, que invoca un tooinstall script WordPress.</span><span class="sxs-lookup"><span data-stu-id="24eaf-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="24eaf-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="24eaf-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="24eaf-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="24eaf-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="24eaf-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24eaf-126">Next steps</span></span>

<span data-ttu-id="24eaf-127">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24eaf-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="24eaf-128">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24eaf-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
