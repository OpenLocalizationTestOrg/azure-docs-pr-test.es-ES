---
title: "una aplicación de la función aaaCreate e implementar código de la función de Visual Studio Team Services | Documentos de Microsoft"
description: "Creación de una instancia de Function App e implementación de código de función desde Visual Studio Team Services"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="0d442-103">Creación de una instancia de App Service</span><span class="sxs-lookup"><span data-stu-id="0d442-103">Create an App Service</span></span>

<span data-ttu-id="0d442-104">En este escenario, aprenderá cómo Hola toocreate una aplicación de función mediante [plan de consumo](../functions-scale.md#consumption-plan) con sus recursos relacionados e implementa continuamente el código de la función desde un repositorio de Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="0d442-104">In this scenario you will learn how toocreate a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="0d442-105">En este ejemplo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0d442-105">In this sample, you will need:</span></span>

* <span data-ttu-id="0d442-106">Un repositorio de VSTS con código de funciones, para el cual tenga permisos administrativos.</span><span class="sxs-lookup"><span data-stu-id="0d442-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="0d442-107">Un [token de acceso personal (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para su cuenta de GitHub.</span><span class="sxs-lookup"><span data-stu-id="0d442-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0d442-108">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0d442-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0d442-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d442-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0d442-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0d442-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0d442-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0d442-111">Sample script</span></span>

<span data-ttu-id="0d442-112">Este ejemplo crea una instancia de Azure Function App e implementa código de la función desde Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0d442-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0d442-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0d442-113">Script explanation</span></span>

<span data-ttu-id="0d442-114">Este script utiliza Hola después comandos toocreate un grupo de recursos, aplicación web, documentos y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="0d442-114">This script uses hello following commands toocreate a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="0d442-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="0d442-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0d442-116">Comando</span><span class="sxs-lookup"><span data-stu-id="0d442-116">Command</span></span> | <span data-ttu-id="0d442-117">Notas</span><span class="sxs-lookup"><span data-stu-id="0d442-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0d442-118">az group create</span><span class="sxs-lookup"><span data-stu-id="0d442-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0d442-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0d442-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0d442-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="0d442-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0d442-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="0d442-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0d442-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="0d442-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="0d442-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="0d442-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="0d442-124">Asocia una aplicación de función con un repositorio GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="0d442-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0d442-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d442-125">Next steps</span></span>

<span data-ttu-id="0d442-126">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0d442-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0d442-127">Encontrará más ejemplos de secuencias de comandos de CLI de funciones de Azure en hello [documentación sobre las funciones de Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0d442-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
