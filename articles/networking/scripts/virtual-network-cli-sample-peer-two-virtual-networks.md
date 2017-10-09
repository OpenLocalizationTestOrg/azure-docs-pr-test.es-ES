---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure del mismo nivel dos redes virtuales | Documentos de Microsoft
description: 'Ejemplo de script de la CLI de Azure: emparejar dos redes virtuales'
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="f1946-103">Conectar dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="f1946-103">Peer two virtual networks</span></span>

<span data-ttu-id="f1946-104">Este script crea y se conecta dos redes virtuales en Hola Hola de trhough región misma red de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1946-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="f1946-105">Después de ejecutar el script de Hola, creará un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="f1946-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="f1946-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f1946-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f1946-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="f1946-107">Clean up deployment</span></span> 

<span data-ttu-id="f1946-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="f1946-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="f1946-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f1946-109">Script explanation</span></span>

<span data-ttu-id="f1946-110">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f1946-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f1946-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="f1946-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f1946-112">Comando</span><span class="sxs-lookup"><span data-stu-id="f1946-112">Command</span></span> | <span data-ttu-id="f1946-113">Notas</span><span class="sxs-lookup"><span data-stu-id="f1946-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1946-114">az group create</span><span class="sxs-lookup"><span data-stu-id="f1946-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f1946-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f1946-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1946-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="f1946-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="f1946-117">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1946-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="f1946-118">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="f1946-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="f1946-119">Crea un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="f1946-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="f1946-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="f1946-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f1946-121">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="f1946-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1946-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1946-122">Next steps</span></span>

<span data-ttu-id="f1946-123">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1946-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f1946-124">Encontrará más ejemplos de secuencias de comandos CLI red Hola [documentación de introducción a las redes Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f1946-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
