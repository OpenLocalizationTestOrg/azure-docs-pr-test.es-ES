---
title: "una aplicación de la función aaaCreate e implementar código de la función desde GitHub | Documentos de Microsoft"
description: "Creación de una aplicación de función e implementación de código de función desde GitHub"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="aebb5-103">Creación de una instancia de App Service</span><span class="sxs-lookup"><span data-stu-id="aebb5-103">Create an App Service</span></span>

<span data-ttu-id="aebb5-104">Este script de ejemplo crea una aplicación de función mediante hello [plan de consumo](../functions-scale.md#consumption-plan) con sus recursos relacionados e implementa continuamente el código de la función desde un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="aebb5-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="aebb5-105">En este ejemplo, necesita:</span><span class="sxs-lookup"><span data-stu-id="aebb5-105">In this sample, you need:</span></span>

* <span data-ttu-id="aebb5-106">Un repositorio de GitHub con código de funciones, para el cual tenga permisos administrativos.</span><span class="sxs-lookup"><span data-stu-id="aebb5-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="aebb5-107">Un [token de acceso personal (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para su cuenta de GitHub.</span><span class="sxs-lookup"><span data-stu-id="aebb5-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aebb5-108">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="aebb5-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="aebb5-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="aebb5-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="aebb5-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aebb5-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="aebb5-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="aebb5-111">Sample script</span></span>

<span data-ttu-id="aebb5-112">Este ejemplo crea una instancia de Azure Function App e implementa código de la función desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="aebb5-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="aebb5-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="aebb5-113">Script explanation</span></span>

<span data-ttu-id="aebb5-114">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="aebb5-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="aebb5-115">Este script utiliza siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="aebb5-115">This script uses hello following:</span></span>

| <span data-ttu-id="aebb5-116">Comando</span><span class="sxs-lookup"><span data-stu-id="aebb5-116">Command</span></span> | <span data-ttu-id="aebb5-117">Notas</span><span class="sxs-lookup"><span data-stu-id="aebb5-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aebb5-118">az group create</span><span class="sxs-lookup"><span data-stu-id="aebb5-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="aebb5-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="aebb5-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="aebb5-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="aebb5-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="aebb5-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="aebb5-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="aebb5-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="aebb5-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="aebb5-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="aebb5-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="aebb5-124">Asocia una aplicación de función con un repositorio GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="aebb5-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aebb5-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aebb5-125">Next steps</span></span>

<span data-ttu-id="aebb5-126">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aebb5-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="aebb5-127">Encontrará más ejemplos de secuencias de comandos de CLI de funciones de Azure en hello [documentación sobre las funciones de Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="aebb5-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
