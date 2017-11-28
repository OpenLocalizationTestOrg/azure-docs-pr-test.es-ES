---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una aplicación web con una implementación continua desde GitHub | Documentos de Microsoft"
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
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="3e071-103">Creación de una aplicación web con implementación continua desde GitHub</span><span class="sxs-lookup"><span data-stu-id="3e071-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="3e071-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, configura la implementación continua desde un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e071-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="3e071-105">Para la implementación de GitHub sin una implementación continua, consulte [Creación de una aplicación web e implementación de código desde GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="3e071-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="3e071-106">En este ejemplo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e071-106">In this sample, you will need:</span></span>

* <span data-ttu-id="3e071-107">Un repositorio de GitHub con código de aplicación, para el cual deberá tener permisos administrativos.</span><span class="sxs-lookup"><span data-stu-id="3e071-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="3e071-108">Un [token de acceso personal (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para su cuenta de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e071-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3e071-109">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="3e071-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3e071-110">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e071-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3e071-111">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3e071-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3e071-112">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3e071-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3e071-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="3e071-113">Script explanation</span></span>

<span data-ttu-id="3e071-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="3e071-114">This script uses hello following commands.</span></span> <span data-ttu-id="3e071-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="3e071-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3e071-116">Comando</span><span class="sxs-lookup"><span data-stu-id="3e071-116">Command</span></span> | <span data-ttu-id="3e071-117">Notas</span><span class="sxs-lookup"><span data-stu-id="3e071-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3e071-118">az group create</span><span class="sxs-lookup"><span data-stu-id="3e071-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3e071-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="3e071-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3e071-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="3e071-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3e071-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="3e071-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3e071-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="3e071-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="3e071-123">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e071-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="3e071-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="3e071-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="3e071-125">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="3e071-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="3e071-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="3e071-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="3e071-127">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="3e071-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3e071-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e071-128">Next steps</span></span>

<span data-ttu-id="3e071-129">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e071-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3e071-130">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3e071-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
