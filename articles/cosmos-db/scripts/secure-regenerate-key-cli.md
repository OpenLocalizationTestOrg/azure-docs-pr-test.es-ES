---
title: clave de cuenta de base de datos de CLI Script Regenerate Azure Cosmos aaaAzure | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: regeneración de una clave de cuenta de Azure Cosmos DB"
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
ms.openlocfilehash: ca77e05039775c90d7541899eeffc45a76d60657
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-hello-azure-cli"></a><span data-ttu-id="20704-103">Volver a generar una clave de cuenta de base de datos de Azure Cosmos mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="20704-103">Regenerate an Azure Cosmos DB account key using hello Azure CLI</span></span>

<span data-ttu-id="20704-104">Este ejemplo vuelve a generar cualquier tipo de clave de cuenta de base de datos de Azure Cosmos utilizando Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="20704-104">This sample regenerates any kind of Azure Cosmos DB account key using hello Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="20704-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="20704-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="20704-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="20704-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="20704-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="20704-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="20704-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="20704-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-regenerate-keys/secure-cosmosdb-regenerate-keys.sh?highlight=27-31 "Regenerate Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="20704-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="20704-109">Clean up deployment</span></span>

<span data-ttu-id="20704-110">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="20704-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="20704-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="20704-111">Script explanation</span></span>

<span data-ttu-id="20704-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="20704-112">This script uses hello following commands.</span></span> <span data-ttu-id="20704-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="20704-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="20704-114">Comando</span><span class="sxs-lookup"><span data-stu-id="20704-114">Command</span></span> | <span data-ttu-id="20704-115">Notas</span><span class="sxs-lookup"><span data-stu-id="20704-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="20704-116">az group create</span><span class="sxs-lookup"><span data-stu-id="20704-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="20704-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="20704-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="20704-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="20704-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="20704-119">Actualiza una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20704-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="20704-120">az cosmosdb regenerate-key</span><span class="sxs-lookup"><span data-stu-id="20704-120">az cosmosdb regenerate-key</span></span>](/cli/azure/cosmosdb/regenerate-key) | <span data-ttu-id="20704-121">Regenera claves de cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20704-121">Regeneratates Azure Cosmos DB account keys.</span></span> |
| [<span data-ttu-id="20704-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="20704-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="20704-123">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="20704-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="20704-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20704-124">Next steps</span></span>

<span data-ttu-id="20704-125">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20704-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="20704-126">Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de Azure Cosmos en hello [documentación de Azure Cosmos DB CLI](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20704-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
