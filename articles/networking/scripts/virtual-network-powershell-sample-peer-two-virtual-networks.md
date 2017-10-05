---
title: 'Ejemplo de script de Azure PowerShell: emparejar dos redes virtuales | Microsoft Docs'
description: 'Ejemplo de script de Azure PowerShell: emparejar dos redes virtuales'
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="4c231-103">Conectar dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="4c231-103">Peer two virtual networks</span></span>

<span data-ttu-id="4c231-104">Este script crea y conecta dos redes virtuales de la misma región a través de la red de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c231-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="4c231-105">Después de ejecutar el script, se creará un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4c231-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="4c231-106">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="4c231-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4c231-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4c231-107">Sample script</span></span>

<span data-ttu-id="4c231-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Emparejar dos redes")]</span><span class="sxs-lookup"><span data-stu-id="4c231-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4c231-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="4c231-109">Clean up deployment</span></span> 

<span data-ttu-id="4c231-110">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4c231-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4c231-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="4c231-111">Script explanation</span></span>

<span data-ttu-id="4c231-112">Este script usa los siguientes comandos para crear un grupo de recursos, una máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4c231-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="4c231-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="4c231-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4c231-114">Comando</span><span class="sxs-lookup"><span data-stu-id="4c231-114">Command</span></span> | <span data-ttu-id="4c231-115">Notas</span><span class="sxs-lookup"><span data-stu-id="4c231-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4c231-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4c231-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4c231-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="4c231-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="4c231-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4c231-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="4c231-119">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c231-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="4c231-120">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="4c231-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="4c231-121">Crea un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4c231-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="4c231-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4c231-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4c231-123">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="4c231-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4c231-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c231-124">Next steps</span></span>

<span data-ttu-id="4c231-125">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4c231-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="4c231-126">En la [documentación de la información general de redes de Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json) puede encontrar ejemplos adicionales de script de PowerShell de redes.</span><span class="sxs-lookup"><span data-stu-id="4c231-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>