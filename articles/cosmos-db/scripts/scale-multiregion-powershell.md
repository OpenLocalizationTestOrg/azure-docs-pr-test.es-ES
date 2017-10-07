---
title: "replicación de aaaAzure Multiregion de secuencia de comandos de PowerShell de la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: replicación en varias regiones para Azure Cosmos DB"
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
ms.openlocfilehash: 8e3e79f086f46fc037d52589eb8bcf4557214566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="0f564-103">Replicación de una cuenta de base de datos de Azure Cosmos DB en varias regiones y configuración de prioridades de conmutación por error mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f564-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="0f564-104">Este ejemplo replica cualquier tipo de cuenta de base de datos de Azure Cosmos DB en varias regiones y configura prioridades de conmutación por error mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f564-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="0f564-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0f564-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0f564-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="0f564-106">Clean up deployment</span></span>

<span data-ttu-id="0f564-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="0f564-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0f564-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0f564-108">Script explanation</span></span>

<span data-ttu-id="0f564-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="0f564-109">This script uses hello following commands.</span></span> <span data-ttu-id="0f564-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="0f564-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0f564-111">Comando</span><span class="sxs-lookup"><span data-stu-id="0f564-111">Command</span></span> | <span data-ttu-id="0f564-112">Notas</span><span class="sxs-lookup"><span data-stu-id="0f564-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0f564-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0f564-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="0f564-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0f564-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0f564-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="0f564-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="0f564-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="0f564-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="0f564-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="0f564-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="0f564-118">Modifica la cuenta de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f564-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="0f564-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0f564-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="0f564-120">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="0f564-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="0f564-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f564-121">Next steps</span></span>

<span data-ttu-id="0f564-122">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="0f564-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="0f564-123">Encontrará más ejemplos de secuencias de comandos de PowerShell de base de datos de Azure Cosmos en hello [scripts de PowerShell de base de datos de Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0f564-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
