---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una aplicación web con una implementación continua desde Visual Studio Team Services | Documentos de Microsoft"
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
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="49960-103">Creación de una aplicación web con implementación continua desde Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="49960-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="49960-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, configura la implementación continua desde un repositorio de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="49960-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="49960-105">Para este ejemplo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="49960-105">For this sample, you will need:</span></span>

* <span data-ttu-id="49960-106">Un repositorio de Visual Studio Team Services con el código de la aplicación, para la cual tendrá que tener permisos administrativos.</span><span class="sxs-lookup"><span data-stu-id="49960-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="49960-107">Un [token de acceso personal (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) para la cuenta de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="49960-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49960-108">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="49960-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="49960-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="49960-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="49960-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="49960-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="49960-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="49960-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="49960-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="49960-112">Script explanation</span></span>

<span data-ttu-id="49960-113">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="49960-113">This script uses hello following commands.</span></span> <span data-ttu-id="49960-114">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="49960-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="49960-115">Comando</span><span class="sxs-lookup"><span data-stu-id="49960-115">Command</span></span> | <span data-ttu-id="49960-116">Notas</span><span class="sxs-lookup"><span data-stu-id="49960-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="49960-117">az group create</span><span class="sxs-lookup"><span data-stu-id="49960-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="49960-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="49960-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="49960-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="49960-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="49960-120">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="49960-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="49960-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="49960-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="49960-122">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="49960-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="49960-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="49960-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="49960-124">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="49960-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="49960-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="49960-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="49960-126">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="49960-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="49960-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49960-127">Next steps</span></span>

<span data-ttu-id="49960-128">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="49960-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="49960-129">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="49960-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
