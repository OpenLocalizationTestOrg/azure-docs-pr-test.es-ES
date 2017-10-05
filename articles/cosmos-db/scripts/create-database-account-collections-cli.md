---
title: "Script de la CLI de Azure: creación de una cuenta, base de datos y colección de API de DocumentDB para Azure Cosmos DB | Microsoft Docs"
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
ms.openlocfilehash: 28f99d56404e47adcd375d9f3106cc234469cbfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="938c9-103">Azure Cosmos DB: creación de una cuenta de API de DocumentDB mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="938c9-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="938c9-104">Este script de ejemplo de la CLI crea una cuenta, base de datos y colección de API de DocumentDB en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="938c9-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="938c9-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="938c9-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="938c9-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="938c9-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="938c9-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="938c9-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="938c9-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="938c9-108">Sample script</span></span>

<span data-ttu-id="938c9-109">[!code-azurecli-interactive[principal](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Creación de una cuenta, base de datos y colección de API de DocumentDB para Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="938c9-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="938c9-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="938c9-110">Clean up deployment</span></span>

<span data-ttu-id="938c9-111">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="938c9-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="938c9-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="938c9-112">Script explanation</span></span>

<span data-ttu-id="938c9-113">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="938c9-113">This script uses the following commands.</span></span> <span data-ttu-id="938c9-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="938c9-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="938c9-115">Comando</span><span class="sxs-lookup"><span data-stu-id="938c9-115">Command</span></span> | <span data-ttu-id="938c9-116">Notas</span><span class="sxs-lookup"><span data-stu-id="938c9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="938c9-117">az group create</span><span class="sxs-lookup"><span data-stu-id="938c9-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="938c9-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="938c9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="938c9-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="938c9-119">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="938c9-120">Crea una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="938c9-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="938c9-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="938c9-121">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="938c9-122">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="938c9-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="938c9-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="938c9-123">Next steps</span></span>

<span data-ttu-id="938c9-124">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="938c9-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="938c9-125">Encontrará más ejemplos de scripts de la CLI de Azure Cosmos DB en la [documentación de la CLI de Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="938c9-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>