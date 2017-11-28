---
title: "aaaAzure ejemplo de secuencia de comandos de CLI: conectar una caché en redis de aplicación web tooa | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: conectar una caché de redis de tooa de aplicación web"
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="e1d4c-103">Conectar una caché de redis de tooa de aplicación web</span><span class="sxs-lookup"><span data-stu-id="e1d4c-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="e1d4c-104">En este escenario, aprenderá cómo toocreate un Azure redis caché y una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="e1d4c-105">A continuación, vinculará Hola redis caché toohello web app con la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e1d4c-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1d4c-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e1d4c-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="e1d4c-107">Script explanation</span></span>

<span data-ttu-id="e1d4c-108">Este script utiliza Hola siga los comandos del toocreate un grupo de recursos, la aplicación web, redis caché y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="e1d4c-109">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e1d4c-110">Comando</span><span class="sxs-lookup"><span data-stu-id="e1d4c-110">Command</span></span> | <span data-ttu-id="e1d4c-111">Notas</span><span class="sxs-lookup"><span data-stu-id="e1d4c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e1d4c-112">az group create</span><span class="sxs-lookup"><span data-stu-id="e1d4c-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e1d4c-113">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e1d4c-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e1d4c-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e1d4c-115">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="e1d4c-115">Creates an App Service plan.</span></span> <span data-ttu-id="e1d4c-116">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e1d4c-117">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e1d4c-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e1d4c-118">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e1d4c-119">az redis create</span><span class="sxs-lookup"><span data-stu-id="e1d4c-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="e1d4c-120">Crea una instancia nueva de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="e1d4c-121">Esto es donde se almacenarán los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="e1d4c-122">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="e1d4c-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="e1d4c-123">Enumera las teclas de acceso de Hola Hola redis la instancia de caché.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="e1d4c-124">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="e1d4c-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="e1d4c-125">Crea o actualiza una configuración de aplicación para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="e1d4c-126">La configuración de la aplicación se expone como variables de entorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1d4c-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e1d4c-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1d4c-127">Next steps</span></span>

<span data-ttu-id="e1d4c-128">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e1d4c-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e1d4c-129">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e1d4c-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
