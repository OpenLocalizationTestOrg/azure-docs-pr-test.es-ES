---
title: clave de cuenta de base de datos de PowerShell Script Regenerate Azure Cosmos aaaAzure | Documentos de Microsoft
description: "Ejemplo de script de Azure PowerShell: regeneración de la clave de cuenta de Azure Cosmos DB"
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
ms.openlocfilehash: 7ac1749a75a12ba7f8ff68e8106c29693490151a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-powershell"></a><span data-ttu-id="3f0f5-103">Regeneración de una clave de cuenta de Azure Cosmos DB mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f0f5-103">Regenerate an Azure Cosmos DB account key using PowerShell</span></span>

<span data-ttu-id="3f0f5-104">Este ejemplo vuelve a generar cualquier tipo de clave de cuenta de base de datos de Azure Cosmos utilizando Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-104">This sample regenerates any kind of Azure Cosmos DB account key using hello Azure CLI.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="3f0f5-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3f0f5-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/regenerate-account-keys/regenerate-account-keys.ps1?highlight=36-41 "Regenerate Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3f0f5-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="3f0f5-106">Clean up deployment</span></span>

<span data-ttu-id="3f0f5-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3f0f5-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="3f0f5-108">Script explanation</span></span>

<span data-ttu-id="3f0f5-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-109">This script uses hello following commands.</span></span> <span data-ttu-id="3f0f5-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3f0f5-111">Comando</span><span class="sxs-lookup"><span data-stu-id="3f0f5-111">Command</span></span> | <span data-ttu-id="3f0f5-112">Notas</span><span class="sxs-lookup"><span data-stu-id="3f0f5-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3f0f5-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3f0f5-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="3f0f5-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3f0f5-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3f0f5-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="3f0f5-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="3f0f5-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="3f0f5-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="3f0f5-118">Se invoca una acción en la cuenta de Azure CosmosDB Hola.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="3f0f5-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3f0f5-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="3f0f5-120">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="3f0f5-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3f0f5-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f0f5-121">Next steps</span></span>

<span data-ttu-id="3f0f5-122">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="3f0f5-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="3f0f5-123">Encontrará más ejemplos de secuencias de comandos de PowerShell de base de datos de Azure Cosmos en hello [scripts de PowerShell de base de datos de Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3f0f5-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
