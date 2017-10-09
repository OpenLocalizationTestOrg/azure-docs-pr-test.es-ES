---
title: un servidor de seguridad de base de datos de Azure Cosmos de crear secuencias de comandos de CLI de aaaAzure | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: creación de un firewall para Azure Cosmos DB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: d4bee4f37906033c96826b9662d2ba396325c792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-hello-azure-cli"></a><span data-ttu-id="39d3d-103">Azure Cosmos DB: Crear un firewall mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="39d3d-103">Azure Cosmos DB: Create a firewall using hello Azure CLI</span></span>

<span data-ttu-id="39d3d-104">Este script de ejemplo de la CLI crea una directiva de firewall para cualquier tipo de cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39d3d-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="39d3d-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="39d3d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="39d3d-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="39d3d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="39d3d-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="39d3d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="39d3d-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="39d3d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]

## <a name="clean-up-deployment"></a><span data-ttu-id="39d3d-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="39d3d-109">Clean up deployment</span></span>

<span data-ttu-id="39d3d-110">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="39d3d-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="39d3d-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="39d3d-111">Script explanation</span></span>

<span data-ttu-id="39d3d-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="39d3d-112">This script uses hello following commands.</span></span> <span data-ttu-id="39d3d-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="39d3d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="39d3d-114">Comando</span><span class="sxs-lookup"><span data-stu-id="39d3d-114">Command</span></span> | <span data-ttu-id="39d3d-115">Notas</span><span class="sxs-lookup"><span data-stu-id="39d3d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39d3d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="39d3d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="39d3d-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="39d3d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="39d3d-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="39d3d-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="39d3d-119">Crea una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39d3d-119">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="39d3d-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="39d3d-120">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="39d3d-121">Actualiza una configuración de firewall de Azure CosmosDB cuenta tooinclude.</span><span class="sxs-lookup"><span data-stu-id="39d3d-121">Updates an Azure CosmosDB account tooinclude firewall settings.</span></span> |
| [<span data-ttu-id="39d3d-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="39d3d-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="39d3d-123">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="39d3d-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39d3d-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39d3d-124">Next steps</span></span>

<span data-ttu-id="39d3d-125">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="39d3d-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="39d3d-126">Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de Azure Cosmos en hello [documentación de Azure Cosmos DB CLI](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="39d3d-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
