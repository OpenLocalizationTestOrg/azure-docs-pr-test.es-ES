---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure de instalar IIS | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: instalación de IIS"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="b5d71-103">Creación rápida de una máquina virtual con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b5d71-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="b5d71-104">Este script crea una máquina Virtual de Azure ejecutando Windows Server 2016 y usa hello tooinstall de extensión de Script personalizado de Azure Máquina Virtual de IIS.</span><span class="sxs-lookup"><span data-stu-id="b5d71-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="b5d71-105">Después de ejecutar el script de Hola, puede tener acceso a sitio Web IIS de hello predeterminado en la dirección IP pública de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d71-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b5d71-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b5d71-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b5d71-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="b5d71-107">Clean up deployment</span></span> 

<span data-ttu-id="b5d71-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="b5d71-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="b5d71-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="b5d71-109">Script explanation</span></span>

<span data-ttu-id="b5d71-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b5d71-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b5d71-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="b5d71-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b5d71-112">Comando</span><span class="sxs-lookup"><span data-stu-id="b5d71-112">Command</span></span> | <span data-ttu-id="b5d71-113">Notas</span><span class="sxs-lookup"><span data-stu-id="b5d71-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b5d71-114">az group create</span><span class="sxs-lookup"><span data-stu-id="b5d71-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b5d71-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="b5d71-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b5d71-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="b5d71-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="b5d71-117">Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="b5d71-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="b5d71-118">Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="b5d71-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="b5d71-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="b5d71-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="b5d71-120">Crea un tooallow de regla de grupo de seguridad de red el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="b5d71-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="b5d71-121">En este ejemplo, el puerto 80 está abierto al tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5d71-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="b5d71-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="b5d71-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b5d71-123">Agrega y se ejecuta un tooa de extensión de máquina virtual VM.</span><span class="sxs-lookup"><span data-stu-id="b5d71-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="b5d71-124">En este ejemplo, la extensión de script personalizado de hello es tooinstall usa IIS.</span><span class="sxs-lookup"><span data-stu-id="b5d71-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="b5d71-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="b5d71-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b5d71-126">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="b5d71-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5d71-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5d71-127">Next steps</span></span>

<span data-ttu-id="b5d71-128">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5d71-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b5d71-129">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5d71-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
