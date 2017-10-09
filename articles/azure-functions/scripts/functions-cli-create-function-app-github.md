---
title: "una aplicación de la función aaaCreate e implementar código de la función desde GitHub | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de una instancia de Function App e implementación de código de función desde GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="e896a-103">Creación de una aplicación de función e implementación de código de función desde GitHub</span><span class="sxs-lookup"><span data-stu-id="e896a-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="e896a-104">Este script de ejemplo crea una aplicación de función mediante hello [plan de consumo](../functions-scale.md#consumption-plan) con sus recursos relacionados e implementa el código de la función desde un repositorio de GitHub público (sin una implementación continua).</span><span class="sxs-lookup"><span data-stu-id="e896a-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="e896a-105">Para la entrega continua del código de la función desde GitHub, lea [Creación de una instancia de Function App e implementación de código de función desde GitHub](functions-cli-create-function-app-github-continuous.md).</span><span class="sxs-lookup"><span data-stu-id="e896a-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e896a-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e896a-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e896a-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e896a-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e896a-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e896a-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e896a-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e896a-109">Sample script</span></span>

<span data-ttu-id="e896a-110">Este ejemplo crea una instancia de Azure Function App e implementa código de la función desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="e896a-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e896a-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="e896a-111">Script explanation</span></span>

<span data-ttu-id="e896a-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="e896a-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="e896a-113">Este script utiliza Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e896a-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="e896a-114">Comando</span><span class="sxs-lookup"><span data-stu-id="e896a-114">Command</span></span> | <span data-ttu-id="e896a-115">Notas</span><span class="sxs-lookup"><span data-stu-id="e896a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e896a-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e896a-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e896a-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="e896a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e896a-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="e896a-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e896a-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="e896a-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e896a-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="e896a-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="e896a-121">Crea una instancia de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="e896a-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="e896a-122">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="e896a-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="e896a-123">Asocia una aplicación de función con un repositorio GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="e896a-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e896a-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e896a-124">Next steps</span></span>

<span data-ttu-id="e896a-125">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e896a-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e896a-126">Encontrará más ejemplos de secuencias de comandos de CLI de funciones de Azure en hello [documentación sobre las funciones de Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e896a-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
