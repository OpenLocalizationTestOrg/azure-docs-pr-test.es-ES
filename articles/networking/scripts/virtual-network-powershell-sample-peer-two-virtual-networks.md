---
title: Ejemplo de Script de PowerShell - aaaAzure del mismo nivel dos redes virtuales | Documentos de Microsoft
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
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="84ee8-103">Conectar dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="84ee8-103">Peer two virtual networks</span></span>

<span data-ttu-id="84ee8-104">Este script crea y se conecta dos redes virtuales en Hola Hola de trhough región misma red de Azure.</span><span class="sxs-lookup"><span data-stu-id="84ee8-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="84ee8-105">Después de ejecutar el script de Hola, creará un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="84ee8-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="84ee8-106">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="84ee8-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="84ee8-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="84ee8-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="84ee8-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="84ee8-108">Clean up deployment</span></span> 

<span data-ttu-id="84ee8-109">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="84ee8-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="84ee8-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="84ee8-110">Script explanation</span></span>

<span data-ttu-id="84ee8-111">Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="84ee8-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="84ee8-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="84ee8-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="84ee8-113">Comando</span><span class="sxs-lookup"><span data-stu-id="84ee8-113">Command</span></span> | <span data-ttu-id="84ee8-114">Notas</span><span class="sxs-lookup"><span data-stu-id="84ee8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="84ee8-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84ee8-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="84ee8-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="84ee8-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="84ee8-117">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="84ee8-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="84ee8-118">Crea una red virtual y una subred de Azure.</span><span class="sxs-lookup"><span data-stu-id="84ee8-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="84ee8-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="84ee8-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="84ee8-120">Crea un emparejamiento entre dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="84ee8-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="84ee8-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84ee8-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="84ee8-122">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="84ee8-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84ee8-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84ee8-123">Next steps</span></span>

<span data-ttu-id="84ee8-124">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="84ee8-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="84ee8-125">Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84ee8-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
