---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una aplicación web con la implementación de GitHub | Documentos de Microsoft"
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
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="e37c9-103">Creación de una aplicación web con implementación desde GitHub</span><span class="sxs-lookup"><span data-stu-id="e37c9-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="e37c9-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web desde un repositorio de GitHub (sin una implementación continua).</span><span class="sxs-lookup"><span data-stu-id="e37c9-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="e37c9-105">Para la implementación de GitHub con una implementación continua, consulte [Creación de una aplicación web con implementación continua desde GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="e37c9-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e37c9-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e37c9-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e37c9-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e37c9-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e37c9-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e37c9-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e37c9-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e37c9-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e37c9-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="e37c9-110">Script explanation</span></span> 

<span data-ttu-id="e37c9-111">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="e37c9-111">This script uses hello following commands.</span></span> <span data-ttu-id="e37c9-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="e37c9-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e37c9-113">Comando</span><span class="sxs-lookup"><span data-stu-id="e37c9-113">Command</span></span> | <span data-ttu-id="e37c9-114">Notas</span><span class="sxs-lookup"><span data-stu-id="e37c9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e37c9-115">az group create</span><span class="sxs-lookup"><span data-stu-id="e37c9-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e37c9-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="e37c9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e37c9-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e37c9-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e37c9-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="e37c9-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e37c9-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e37c9-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e37c9-120">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e37c9-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e37c9-121">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="e37c9-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="e37c9-122">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="e37c9-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="e37c9-123">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="e37c9-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="e37c9-124">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="e37c9-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e37c9-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e37c9-125">Next steps</span></span>

<span data-ttu-id="e37c9-126">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e37c9-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e37c9-127">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e37c9-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
