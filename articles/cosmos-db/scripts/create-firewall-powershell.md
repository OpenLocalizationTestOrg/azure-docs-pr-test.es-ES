---
title: "Script de Azure PowerShell: creación de un firewall para Azure Cosmos DB | Microsoft Docs"
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
ms.openlocfilehash: caad9212649dd3dc47ddb21555b5b8496c3d2da1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="cb7b5-103">Azure Cosmos DB: creación de un firewall con PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb7b5-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="cb7b5-104">Este script de ejemplo de PowerShell crea un firewall para cualquier tipo de cuenta de API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="cb7b5-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cb7b5-105">Sample script</span></span>

<span data-ttu-id="cb7b5-106">[!code-powershell[principal](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Creación de un firewall para Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="cb7b5-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="cb7b5-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="cb7b5-107">Clean up deployment</span></span>

<span data-ttu-id="cb7b5-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="cb7b5-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="cb7b5-109">Script explanation</span></span>

<span data-ttu-id="cb7b5-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-110">This script uses the following commands.</span></span> <span data-ttu-id="cb7b5-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cb7b5-112">Comando</span><span class="sxs-lookup"><span data-stu-id="cb7b5-112">Command</span></span> | <span data-ttu-id="cb7b5-113">Notas</span><span class="sxs-lookup"><span data-stu-id="cb7b5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cb7b5-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb7b5-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="cb7b5-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cb7b5-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="cb7b5-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="cb7b5-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="cb7b5-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="cb7b5-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="cb7b5-119">Modifica la cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="cb7b5-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb7b5-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="cb7b5-121">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="cb7b5-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="cb7b5-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb7b5-122">Next steps</span></span>

<span data-ttu-id="cb7b5-123">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="cb7b5-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="cb7b5-124">Encontrará más ejemplos de scripts de PowerShell de Azure Cosmos DB en los [scripts de PowerShell de Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cb7b5-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>