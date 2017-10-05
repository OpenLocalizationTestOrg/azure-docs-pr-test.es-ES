---
title: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación desde GitHub | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación desde GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="16540-103">Creación de una aplicación web con implementación desde GitHub</span><span class="sxs-lookup"><span data-stu-id="16540-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="16540-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web desde un repositorio de GitHub (sin una implementación continua).</span><span class="sxs-lookup"><span data-stu-id="16540-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="16540-105">Para la implementación de GitHub con una implementación continua, consulte [Creación de una aplicación web con implementación continua desde GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="16540-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="16540-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="16540-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="16540-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="16540-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="16540-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="16540-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="16540-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="16540-109">Sample script</span></span>

<span data-ttu-id="16540-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Creación de una aplicación web con implementación desde GitHub")]</span><span class="sxs-lookup"><span data-stu-id="16540-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="16540-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="16540-111">Script explanation</span></span> 

<span data-ttu-id="16540-112">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="16540-112">This script uses the following commands.</span></span> <span data-ttu-id="16540-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="16540-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="16540-114">Comando</span><span class="sxs-lookup"><span data-stu-id="16540-114">Command</span></span> | <span data-ttu-id="16540-115">Notas</span><span class="sxs-lookup"><span data-stu-id="16540-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16540-116">az group create</span><span class="sxs-lookup"><span data-stu-id="16540-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="16540-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="16540-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="16540-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="16540-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="16540-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="16540-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="16540-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="16540-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="16540-121">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="16540-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="16540-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="16540-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="16540-123">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="16540-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="16540-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="16540-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="16540-125">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="16540-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="16540-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16540-126">Next steps</span></span>

<span data-ttu-id="16540-127">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="16540-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="16540-128">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="16540-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
