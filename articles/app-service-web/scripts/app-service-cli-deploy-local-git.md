---
title: "aaaAzure ejemplo de secuencia de comandos de CLI: crear una aplicación web e implementar código desde un repositorio Git local | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web e implementación de código desde un repositorio local de Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="ee1ae-103">Creación de una aplicación web e implementación de código desde un repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="ee1ae-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="ee1ae-104">Este script de ejemplo crea una aplicación web en App Service con sus recursos relacionados y, después, implementa el código de la aplicación web en un repositorio local de GitHub.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ee1ae-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ee1ae-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ee1ae-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ee1ae-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ee1ae-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee1ae-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ee1ae-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="ee1ae-109">Script explanation</span></span>

<span data-ttu-id="ee1ae-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-110">This script uses hello following commands.</span></span> <span data-ttu-id="ee1ae-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ee1ae-112">Comando</span><span class="sxs-lookup"><span data-stu-id="ee1ae-112">Command</span></span> | <span data-ttu-id="ee1ae-113">Notas</span><span class="sxs-lookup"><span data-stu-id="ee1ae-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ee1ae-114">az group create</span><span class="sxs-lookup"><span data-stu-id="ee1ae-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ee1ae-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ee1ae-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ee1ae-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ee1ae-117">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="ee1ae-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ee1ae-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ee1ae-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ee1ae-119">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ee1ae-120">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="ee1ae-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="ee1ae-121">Establece las credenciales de la implementación de nivel de cuenta de hello para el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="ee1ae-122">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="ee1ae-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="ee1ae-123">Crea una configuración de control de código fuente para un repositorio GIT local.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="ee1ae-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="ee1ae-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="ee1ae-125">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="ee1ae-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ee1ae-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee1ae-126">Next steps</span></span>

<span data-ttu-id="ee1ae-127">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ee1ae-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ee1ae-128">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ee1ae-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
