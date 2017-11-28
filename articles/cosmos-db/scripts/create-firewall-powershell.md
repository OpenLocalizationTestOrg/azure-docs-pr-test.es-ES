---
title: aaaAzure un firewall para la base de datos de Azure Cosmos de crear Script de PowerShell | Documentos de Microsoft
description: "Ejemplo de script de Azure PowerShell: creación de un firewall para Azure Cosmos DB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 00dd2dd847c7ed0e35f5555c2b87b90977f137f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="d1364-103">Azure Cosmos DB: creación de un firewall con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1364-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="d1364-104">Este script de ejemplo de PowerShell crea un firewall para cualquier tipo de cuenta de API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d1364-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d1364-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d1364-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d1364-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="d1364-106">Clean up deployment</span></span>

<span data-ttu-id="d1364-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="d1364-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d1364-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d1364-108">Script explanation</span></span>

<span data-ttu-id="d1364-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="d1364-109">This script uses hello following commands.</span></span> <span data-ttu-id="d1364-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="d1364-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d1364-111">Comando</span><span class="sxs-lookup"><span data-stu-id="d1364-111">Command</span></span> | <span data-ttu-id="d1364-112">Notas</span><span class="sxs-lookup"><span data-stu-id="d1364-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1364-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d1364-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="d1364-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d1364-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d1364-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d1364-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="d1364-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="d1364-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d1364-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="d1364-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="d1364-118">Modifica la cuenta de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1364-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="d1364-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d1364-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="d1364-120">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="d1364-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d1364-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1364-121">Next steps</span></span>

<span data-ttu-id="d1364-122">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="d1364-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="d1364-123">Encontrará más ejemplos de secuencias de comandos de PowerShell de base de datos de Azure Cosmos en hello [scripts de PowerShell de base de datos de Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d1364-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
