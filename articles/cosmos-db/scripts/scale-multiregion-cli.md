---
title: "Script de la CLI de Azure: replicación en varias regiones para Azure Cosmos DB | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: replicación en varias regiones para Azure Cosmos DB"
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
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: ab716c28b88412438d0cea80377f9f0f40dc8bd6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-the-azure-cli"></a><span data-ttu-id="6b49b-103">Replicación de una cuenta de base de datos de Azure Cosmos DB y configuración de prioridades de conmutación por error mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6b49b-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using the Azure CLI</span></span>

<span data-ttu-id="6b49b-104">Este ejemplo replica cualquier tipo de cuenta de base de datos de Azure Cosmos DB en varias regiones y configura prioridades de conmutación por error mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b49b-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using the Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b49b-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="6b49b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6b49b-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="6b49b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6b49b-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b49b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6b49b-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6b49b-108">Sample script</span></span>

<span data-ttu-id="6b49b-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Escalado de Azure Cosmos DB en varias regiones")]</span><span class="sxs-lookup"><span data-stu-id="6b49b-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6b49b-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="6b49b-110">Clean up deployment</span></span>

<span data-ttu-id="6b49b-111">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="6b49b-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6b49b-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6b49b-112">Script explanation</span></span>

<span data-ttu-id="6b49b-113">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="6b49b-113">This script uses the following commands.</span></span> <span data-ttu-id="6b49b-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="6b49b-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6b49b-115">Comando</span><span class="sxs-lookup"><span data-stu-id="6b49b-115">Command</span></span> | <span data-ttu-id="6b49b-116">Notas</span><span class="sxs-lookup"><span data-stu-id="6b49b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6b49b-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6b49b-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6b49b-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6b49b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6b49b-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="6b49b-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="6b49b-120">Actualiza una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6b49b-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="6b49b-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="6b49b-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="6b49b-122">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="6b49b-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6b49b-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b49b-123">Next steps</span></span>

<span data-ttu-id="6b49b-124">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6b49b-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6b49b-125">Encontrará más ejemplos de scripts de la CLI de Azure Cosmos DB en la [documentación de la CLI de Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6b49b-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
