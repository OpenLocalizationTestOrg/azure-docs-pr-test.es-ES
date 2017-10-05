---
title: "Script de la CLI de Azure: obtención de la cadena de conexión de Azure Cosmos DB para aplicaciones MongoDB | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: obtención de la cadena de conexión de Azure Cosmos DB para aplicaciones MongoDB"
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
ms.openlocfilehash: 916c92cab39306352fdf9dff0e0685fd61832d16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-the-azure-cli"></a><span data-ttu-id="9590c-103">Obtención de una cadena de conexión de Azure Cosmos DB para aplicaciones MongoDB mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9590c-103">Get an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI</span></span>

<span data-ttu-id="9590c-104">Este ejemplo obtiene una cadena de conexión de Azure Cosmos DB para aplicaciones MongoDB mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9590c-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9590c-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9590c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9590c-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="9590c-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="9590c-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9590c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9590c-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9590c-108">Sample script</span></span>

<span data-ttu-id="9590c-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Obtención de la cadena de conexión de Azure Cosmos DB para aplicaciones MongoDB")]</span><span class="sxs-lookup"><span data-stu-id="9590c-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9590c-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="9590c-110">Clean up deployment</span></span>

<span data-ttu-id="9590c-111">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="9590c-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9590c-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="9590c-112">Script explanation</span></span>

<span data-ttu-id="9590c-113">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="9590c-113">This script uses the following commands.</span></span> <span data-ttu-id="9590c-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="9590c-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9590c-115">Comando</span><span class="sxs-lookup"><span data-stu-id="9590c-115">Command</span></span> | <span data-ttu-id="9590c-116">Notas</span><span class="sxs-lookup"><span data-stu-id="9590c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9590c-117">az group create</span><span class="sxs-lookup"><span data-stu-id="9590c-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9590c-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="9590c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9590c-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="9590c-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="9590c-120">Actualiza una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9590c-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="9590c-121">az cosmosdb list-connection-strings</span><span class="sxs-lookup"><span data-stu-id="9590c-121">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="9590c-122">Obtiene la cadena de conexión para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="9590c-122">Gets the connection string for the account.</span></span>|
| [<span data-ttu-id="9590c-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="9590c-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="9590c-124">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="9590c-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9590c-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9590c-125">Next steps</span></span>

<span data-ttu-id="9590c-126">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9590c-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9590c-127">Encontrará más ejemplos de scripts de la CLI de Azure Cosmos DB en la [documentación de la CLI de Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9590c-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
