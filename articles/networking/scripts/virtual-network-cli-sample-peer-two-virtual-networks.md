---
title: 'Ejemplo de script de la CLI de Azure: emparejar dos redes virtuales | Microsoft Docs'
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
ms.openlocfilehash: a2b8fda288072e2fb0087988bbd68d3e4d9031d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="04af1-103">Conectar dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="04af1-103">Peer two virtual networks</span></span>

<span data-ttu-id="04af1-104">Este script crea y conecta dos redes virtuales de la misma región a través de la red de Azure.</span><span class="sxs-lookup"><span data-stu-id="04af1-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="04af1-105">Después de ejecutar el script, se creará un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="04af1-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="04af1-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="04af1-106">Sample script</span></span>

<span data-ttu-id="04af1-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Emparejar dos redes")]</span><span class="sxs-lookup"><span data-stu-id="04af1-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="04af1-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="04af1-108">Clean up deployment</span></span> 

<span data-ttu-id="04af1-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="04af1-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="04af1-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="04af1-110">Script explanation</span></span>

<span data-ttu-id="04af1-111">Este script usa los siguientes comandos para crear un grupo de recursos, una máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="04af1-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="04af1-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="04af1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="04af1-113">Comando</span><span class="sxs-lookup"><span data-stu-id="04af1-113">Command</span></span> | <span data-ttu-id="04af1-114">Notas</span><span class="sxs-lookup"><span data-stu-id="04af1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="04af1-115">az group create</span><span class="sxs-lookup"><span data-stu-id="04af1-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="04af1-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="04af1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="04af1-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="04af1-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="04af1-118">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="04af1-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="04af1-119">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="04af1-119">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="04af1-120">Crea un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="04af1-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="04af1-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="04af1-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="04af1-122">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="04af1-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="04af1-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04af1-123">Next steps</span></span>

<span data-ttu-id="04af1-124">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04af1-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="04af1-125">En la [documentación de la información general de redes de Azure](../cli-samples.md) puede encontrar ejemplos adicionales de script de la CLI de redes.</span><span class="sxs-lookup"><span data-stu-id="04af1-125">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
