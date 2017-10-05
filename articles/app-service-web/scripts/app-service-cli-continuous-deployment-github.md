---
title: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación continua desde GitHub | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación continua desde GitHub | Microsoft Docs"
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="f0f2c-103">Creación de una aplicación web con implementación continua desde GitHub</span><span class="sxs-lookup"><span data-stu-id="f0f2c-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="f0f2c-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, configura la implementación continua desde un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="f0f2c-105">Para la implementación de GitHub sin una implementación continua, consulte [Creación de una aplicación web e implementación de código desde GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="f0f2c-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="f0f2c-106">En este ejemplo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f0f2c-106">In this sample, you will need:</span></span>

* <span data-ttu-id="f0f2c-107">Un repositorio de GitHub con código de aplicación, para el cual deberá tener permisos administrativos.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="f0f2c-108">Un [token de acceso personal (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para su cuenta de GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f0f2c-109">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f0f2c-110">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="f0f2c-111">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f0f2c-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f0f2c-112">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f0f2c-112">Sample script</span></span>

<span data-ttu-id="f0f2c-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Creación de una aplicación web con implementación continua desde GitHub")]</span><span class="sxs-lookup"><span data-stu-id="f0f2c-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f0f2c-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f0f2c-114">Script explanation</span></span>

<span data-ttu-id="f0f2c-115">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-115">This script uses the following commands.</span></span> <span data-ttu-id="f0f2c-116">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f0f2c-117">Comando</span><span class="sxs-lookup"><span data-stu-id="f0f2c-117">Command</span></span> | <span data-ttu-id="f0f2c-118">Notas</span><span class="sxs-lookup"><span data-stu-id="f0f2c-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0f2c-119">az group create</span><span class="sxs-lookup"><span data-stu-id="f0f2c-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f0f2c-120">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f0f2c-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f0f2c-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f0f2c-122">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="f0f2c-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f0f2c-123">az webapp create</span><span class="sxs-lookup"><span data-stu-id="f0f2c-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="f0f2c-124">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="f0f2c-125">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="f0f2c-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="f0f2c-126">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="f0f2c-127">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="f0f2c-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="f0f2c-128">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="f0f2c-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0f2c-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0f2c-129">Next steps</span></span>

<span data-ttu-id="f0f2c-130">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0f2c-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f0f2c-131">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f0f2c-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
