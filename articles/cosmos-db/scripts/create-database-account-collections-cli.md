---
title: "aaaAzure secuencia de comandos de CLI: crear una cuenta, base de datos y colección de API de documentos de base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de una cuenta, base de datos y colección de API de DocumentDB para Azure Cosmos DB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/06/2017
ms.author: mimig
ms.openlocfilehash: 53919a849e04fa69680219e51c0289b9f2affe07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="5b0fa-103">Azure Cosmos DB: creación de una cuenta de API de DocumentDB mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="5b0fa-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="5b0fa-104">Este script de ejemplo de la CLI crea una cuenta, base de datos y colección de API de DocumentDB en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5b0fa-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5b0fa-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5b0fa-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5b0fa-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5b0fa-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b0fa-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5b0fa-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5b0fa-109">Clean up deployment</span></span>

<span data-ttu-id="5b0fa-110">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5b0fa-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5b0fa-111">Script explanation</span></span>

<span data-ttu-id="5b0fa-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-112">This script uses hello following commands.</span></span> <span data-ttu-id="5b0fa-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5b0fa-114">Comando</span><span class="sxs-lookup"><span data-stu-id="5b0fa-114">Command</span></span> | <span data-ttu-id="5b0fa-115">Notas</span><span class="sxs-lookup"><span data-stu-id="5b0fa-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5b0fa-116">az group create</span><span class="sxs-lookup"><span data-stu-id="5b0fa-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="5b0fa-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5b0fa-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="5b0fa-118">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="5b0fa-119">Crea una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="5b0fa-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="5b0fa-120">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="5b0fa-121">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="5b0fa-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5b0fa-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b0fa-122">Next steps</span></span>

<span data-ttu-id="5b0fa-123">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5b0fa-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5b0fa-124">Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de Azure Cosmos en hello [documentación de Azure Cosmos DB CLI](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5b0fa-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
