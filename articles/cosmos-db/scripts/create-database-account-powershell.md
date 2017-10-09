---
title: aaaAzure una cuenta de la API de documentos de base de datos de Azure Cosmos de crear Script de PowerShell | Documentos de Microsoft
description: "Ejemplo de script de Azure PowerShell: creación de una cuenta de API de DocumentDB para Azure Cosmos DB"
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
ms.openlocfilehash: f0751faeca3c1de5906b675e736c58f3d5beaea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="0ddd2-103">Azure Cosmos DB: creación de una cuenta de API de DocumentDB mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ddd2-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="0ddd2-104">Este script de ejemplo de PowerShell crea una cuenta de API para Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0ddd2-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="0ddd2-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0ddd2-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0ddd2-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="0ddd2-106">Clean up deployment</span></span>

<span data-ttu-id="0ddd2-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="0ddd2-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0ddd2-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0ddd2-108">Script explanation</span></span>

<span data-ttu-id="0ddd2-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="0ddd2-109">This script uses hello following commands.</span></span> <span data-ttu-id="0ddd2-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="0ddd2-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0ddd2-111">Comando</span><span class="sxs-lookup"><span data-stu-id="0ddd2-111">Command</span></span> | <span data-ttu-id="0ddd2-112">Notas</span><span class="sxs-lookup"><span data-stu-id="0ddd2-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0ddd2-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ddd2-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="0ddd2-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0ddd2-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0ddd2-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="0ddd2-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="0ddd2-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="0ddd2-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="0ddd2-117">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ddd2-117">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="0ddd2-118">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="0ddd2-118">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="0ddd2-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ddd2-119">Next steps</span></span>

<span data-ttu-id="0ddd2-120">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="0ddd2-120">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="0ddd2-121">Encontrará más ejemplos de secuencias de comandos de PowerShell de base de datos de Azure Cosmos en hello [scripts de PowerShell de base de datos de Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0ddd2-121">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
