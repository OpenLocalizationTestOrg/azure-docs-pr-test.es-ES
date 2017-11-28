---
title: "Creación de una aplicación de función e implementación de código de función desde GitHub | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una instancia de Function App e implementación de código de función desde GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="190b4-103">Creación de una aplicación de función e implementación de código de función desde GitHub</span><span class="sxs-lookup"><span data-stu-id="190b4-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="190b4-104">Este script de ejemplo crea una aplicación de función usando el [plan de consumo](../functions-scale.md#consumption-plan) con sus recursos relacionados e implementa el código de la función desde un repositorio público de GitHub (sin implementación continua).</span><span class="sxs-lookup"><span data-stu-id="190b4-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="190b4-105">Para la entrega continua del código de la función desde GitHub, lea [Creación de una instancia de Function App e implementación de código de función desde GitHub](functions-cli-create-function-app-github-continuous.md).</span><span class="sxs-lookup"><span data-stu-id="190b4-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="190b4-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="190b4-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="190b4-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="190b4-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="190b4-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="190b4-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="190b4-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="190b4-109">Sample script</span></span>

<span data-ttu-id="190b4-110">Este ejemplo crea una instancia de Azure Function App e implementa código de la función desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="190b4-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="190b4-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Creación de una aplicación de función con implementación desde GitHub")]</span><span class="sxs-lookup"><span data-stu-id="190b4-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="190b4-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="190b4-112">Script explanation</span></span>

<span data-ttu-id="190b4-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="190b4-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="190b4-114">Este script usa los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="190b4-114">This script uses the following commands:</span></span>

| <span data-ttu-id="190b4-115">Comando</span><span class="sxs-lookup"><span data-stu-id="190b4-115">Command</span></span> | <span data-ttu-id="190b4-116">Notas</span><span class="sxs-lookup"><span data-stu-id="190b4-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="190b4-117">az group create</span><span class="sxs-lookup"><span data-stu-id="190b4-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="190b4-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="190b4-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="190b4-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="190b4-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="190b4-120">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="190b4-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="190b4-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="190b4-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="190b4-122">Crea una instancia de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="190b4-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="190b4-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="190b4-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="190b4-124">Asocia una aplicación de función con un repositorio GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="190b4-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="190b4-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="190b4-125">Next steps</span></span>

<span data-ttu-id="190b4-126">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="190b4-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="190b4-127">Encontrará más ejemplos de scripts de CLI para Azure Functions en la [documentación de Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="190b4-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
