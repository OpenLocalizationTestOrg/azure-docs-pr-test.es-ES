---
title: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a Cosmos DB | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a Cosmos DB"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="85f2a-103">Conexión de una aplicación web a Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85f2a-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="85f2a-104">En este escenario aprenderá a crear una cuenta de Cosmos DB y una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="85f2a-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="85f2a-105">Luego, vinculará la instancia de Cosmos DB a la aplicación web mediante la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85f2a-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="85f2a-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="85f2a-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="85f2a-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="85f2a-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="85f2a-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="85f2a-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="85f2a-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="85f2a-109">Sample script</span></span>

<span data-ttu-id="85f2a-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="85f2a-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="85f2a-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="85f2a-111">Script explanation</span></span>

<span data-ttu-id="85f2a-112">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web, Cosmos DB y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="85f2a-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="85f2a-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="85f2a-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="85f2a-114">Comando</span><span class="sxs-lookup"><span data-stu-id="85f2a-114">Command</span></span> | <span data-ttu-id="85f2a-115">Notas</span><span class="sxs-lookup"><span data-stu-id="85f2a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="85f2a-116">az group create</span><span class="sxs-lookup"><span data-stu-id="85f2a-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="85f2a-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="85f2a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="85f2a-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="85f2a-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="85f2a-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="85f2a-119">Creates an App Service plan.</span></span> <span data-ttu-id="85f2a-120">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="85f2a-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="85f2a-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="85f2a-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="85f2a-122">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="85f2a-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="85f2a-123">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="85f2a-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="85f2a-124">Crea una cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85f2a-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="85f2a-125">Aquí es donde se almacenarán los datos.</span><span class="sxs-lookup"><span data-stu-id="85f2a-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="85f2a-126">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="85f2a-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="85f2a-127">Devuelve las claves de acceso de la cuenta de Cosmos DB especificada.</span><span class="sxs-lookup"><span data-stu-id="85f2a-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="85f2a-128">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="85f2a-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="85f2a-129">Crea o actualiza una configuración de aplicación para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="85f2a-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="85f2a-130">La configuración de la aplicación se expone como variables de entorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="85f2a-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85f2a-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85f2a-131">Next steps</span></span>

<span data-ttu-id="85f2a-132">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85f2a-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="85f2a-133">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="85f2a-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
