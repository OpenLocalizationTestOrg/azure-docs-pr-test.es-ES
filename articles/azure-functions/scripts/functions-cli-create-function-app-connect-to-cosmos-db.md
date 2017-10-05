---
title: "Creación de una función de Azure que se conecta a una instancia de Azure Cosmos DB | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una función de Azure que se conecta a una instancia de Azure Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="31fda-103">Creación de una función de Azure que se conecta a una instancia de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="31fda-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="31fda-104">Este script de ejemplo crea una instancia de Azure Function App y la conecta a una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="31fda-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="31fda-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="31fda-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="31fda-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="31fda-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="31fda-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="31fda-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="31fda-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="31fda-108">Sample script</span></span>

<span data-ttu-id="31fda-109">Este ejemplo crea una aplicación de Azure Function App y agrega una clave de acceso y un punto de conexión de Cosmos DB a configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31fda-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="31fda-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Creación de una función de Azure que se conecta a una instancia de Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="31fda-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="31fda-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="31fda-111">Clean up deployment</span></span>

<span data-ttu-id="31fda-112">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="31fda-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="31fda-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="31fda-113">Script explanation</span></span>

<span data-ttu-id="31fda-114">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="31fda-114">This script uses the following commands.</span></span> <span data-ttu-id="31fda-115">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="31fda-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="31fda-116">Comando</span><span class="sxs-lookup"><span data-stu-id="31fda-116">Command</span></span> | <span data-ttu-id="31fda-117">Notas</span><span class="sxs-lookup"><span data-stu-id="31fda-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="31fda-118">az login</span><span class="sxs-lookup"><span data-stu-id="31fda-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="31fda-119">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="31fda-119">Login to Azure.</span></span> |
| [<span data-ttu-id="31fda-120">az group create</span><span class="sxs-lookup"><span data-stu-id="31fda-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="31fda-121">Crea un grupo de recursos con una ubicación.</span><span class="sxs-lookup"><span data-stu-id="31fda-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="31fda-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="31fda-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="31fda-123">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="31fda-123">Create a storage account</span></span> |
| [<span data-ttu-id="31fda-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="31fda-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="31fda-125">Crea una nueva instancia de Function App.</span><span class="sxs-lookup"><span data-stu-id="31fda-125">Create a new function app</span></span> |
| [<span data-ttu-id="31fda-126">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="31fda-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="31fda-127">Crea una base de datos de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="31fda-127">Create documentdb database</span></span> |
| [<span data-ttu-id="31fda-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="31fda-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="31fda-129">Limpieza</span><span class="sxs-lookup"><span data-stu-id="31fda-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="31fda-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="31fda-130">Next steps</span></span>

<span data-ttu-id="31fda-131">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="31fda-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="31fda-132">Encontrará más ejemplos de scripts de CLI para Azure Functions en la [documentación de Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="31fda-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




