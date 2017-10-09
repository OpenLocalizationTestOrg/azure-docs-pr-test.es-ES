---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure conectarse un tooCosmos de aplicación web DB | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: conectar un tooCosmos de aplicación web DB"
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
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="2932f-103">Conectar un tooCosmos de aplicación web DB</span><span class="sxs-lookup"><span data-stu-id="2932f-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="2932f-104">En este escenario, aprenderá cómo toocreate una cuenta de base de datos de Azure Cosmos y un Azure aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2932f-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="2932f-105">A continuación, vinculará Hola DB Cosmos toohello web app con la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2932f-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2932f-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2932f-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2932f-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2932f-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2932f-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2932f-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2932f-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2932f-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2932f-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2932f-110">Script explanation</span></span>

<span data-ttu-id="2932f-111">Este script utiliza Hola después comandos toocreate un grupo de recursos, aplicación web, base de datos de Cosmos y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="2932f-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="2932f-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="2932f-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2932f-113">Comando</span><span class="sxs-lookup"><span data-stu-id="2932f-113">Command</span></span> | <span data-ttu-id="2932f-114">Notas</span><span class="sxs-lookup"><span data-stu-id="2932f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2932f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="2932f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2932f-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="2932f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2932f-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="2932f-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2932f-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="2932f-118">Creates an App Service plan.</span></span> <span data-ttu-id="2932f-119">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2932f-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="2932f-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="2932f-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="2932f-121">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2932f-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="2932f-122">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="2932f-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="2932f-123">Crea una cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2932f-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="2932f-124">Esto es donde se almacenarán los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2932f-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="2932f-125">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="2932f-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="2932f-126">Teclas de acceso de Hola de listas de Hola la cuenta de base de datos de Cosmos especifican.</span><span class="sxs-lookup"><span data-stu-id="2932f-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="2932f-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="2932f-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="2932f-128">Crea o actualiza una configuración de aplicación para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2932f-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="2932f-129">La configuración de la aplicación se expone como variables de entorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2932f-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2932f-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2932f-130">Next steps</span></span>

<span data-ttu-id="2932f-131">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2932f-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2932f-132">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2932f-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
