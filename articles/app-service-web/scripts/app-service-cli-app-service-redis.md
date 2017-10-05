---
title: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a Redis Cache | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a Redis Cache"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="44dcb-103">Conexión de una aplicación web a Redis Cache</span><span class="sxs-lookup"><span data-stu-id="44dcb-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="44dcb-104">En este escenario aprenderá a crear una instancia de Azure Redis Cache y una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="44dcb-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="44dcb-105">Y, después, vinculará la instancia de Redis Cache a la aplicación web mediante la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44dcb-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="44dcb-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="44dcb-106">Sample script</span></span>

<span data-ttu-id="44dcb-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="44dcb-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="44dcb-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="44dcb-108">Script explanation</span></span>

<span data-ttu-id="44dcb-109">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web, una instancia de Redis Cache y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="44dcb-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="44dcb-110">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="44dcb-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="44dcb-111">Comando</span><span class="sxs-lookup"><span data-stu-id="44dcb-111">Command</span></span> | <span data-ttu-id="44dcb-112">Notas</span><span class="sxs-lookup"><span data-stu-id="44dcb-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="44dcb-113">az group create</span><span class="sxs-lookup"><span data-stu-id="44dcb-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="44dcb-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="44dcb-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="44dcb-115">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="44dcb-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="44dcb-116">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="44dcb-116">Creates an App Service plan.</span></span> <span data-ttu-id="44dcb-117">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="44dcb-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="44dcb-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="44dcb-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="44dcb-119">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="44dcb-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="44dcb-120">az redis create</span><span class="sxs-lookup"><span data-stu-id="44dcb-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="44dcb-121">Crea una instancia nueva de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="44dcb-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="44dcb-122">Aquí es donde se almacenarán los datos.</span><span class="sxs-lookup"><span data-stu-id="44dcb-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="44dcb-123">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="44dcb-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="44dcb-124">Muestra las teclas de acceso de la instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="44dcb-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="44dcb-125">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="44dcb-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="44dcb-126">Crea o actualiza una configuración de aplicación para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="44dcb-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="44dcb-127">La configuración de la aplicación se expone como variables de entorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44dcb-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44dcb-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44dcb-128">Next steps</span></span>

<span data-ttu-id="44dcb-129">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44dcb-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="44dcb-130">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="44dcb-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
