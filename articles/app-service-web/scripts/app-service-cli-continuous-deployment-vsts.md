---
title: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación continua desde Visual Studio Team Services | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web con implementación continua desde Visual Studio Team Services"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="a70ee-103">Creación de una aplicación web con implementación continua desde Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a70ee-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="a70ee-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, configura la implementación continua desde un repositorio de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a70ee-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="a70ee-105">Para este ejemplo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a70ee-105">For this sample, you will need:</span></span>

* <span data-ttu-id="a70ee-106">Un repositorio de Visual Studio Team Services con el código de la aplicación, para la cual tendrá que tener permisos administrativos.</span><span class="sxs-lookup"><span data-stu-id="a70ee-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="a70ee-107">Un [token de acceso personal (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) para la cuenta de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a70ee-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a70ee-108">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a70ee-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a70ee-109">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="a70ee-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="a70ee-110">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a70ee-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a70ee-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a70ee-111">Sample script</span></span>

<span data-ttu-id="a70ee-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Creación de una aplicación web con implementación continua desde Visual Studio Team Services")]</span><span class="sxs-lookup"><span data-stu-id="a70ee-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a70ee-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="a70ee-113">Script explanation</span></span>

<span data-ttu-id="a70ee-114">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="a70ee-114">This script uses the following commands.</span></span> <span data-ttu-id="a70ee-115">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="a70ee-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a70ee-116">Comando</span><span class="sxs-lookup"><span data-stu-id="a70ee-116">Command</span></span> | <span data-ttu-id="a70ee-117">Notas</span><span class="sxs-lookup"><span data-stu-id="a70ee-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a70ee-118">az group create</span><span class="sxs-lookup"><span data-stu-id="a70ee-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a70ee-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="a70ee-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a70ee-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a70ee-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a70ee-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="a70ee-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a70ee-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="a70ee-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a70ee-123">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="a70ee-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a70ee-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="a70ee-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="a70ee-125">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="a70ee-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="a70ee-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="a70ee-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="a70ee-127">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="a70ee-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a70ee-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a70ee-128">Next steps</span></span>

<span data-ttu-id="a70ee-129">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a70ee-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a70ee-130">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a70ee-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
