---
title: "Ejemplo de script de la CLI de Azure: creación de una instancia de Function App en un plan de App Service | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una instancia de Function App en un plan de App Service"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="ae573-103">Creación de una instancia de Function App en un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="ae573-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="ae573-104">Este script de ejemplo crea una instancia de Azure Function App, que es un contenedor para las funciones.</span><span class="sxs-lookup"><span data-stu-id="ae573-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="ae573-105">La instancia de Function App se creará usando un plan de App Service dedicado, lo que significa que los recursos del servidor están siempre disponibles.</span><span class="sxs-lookup"><span data-stu-id="ae573-105">The Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ae573-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ae573-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ae573-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="ae573-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="ae573-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ae573-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ae573-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ae573-109">Sample script</span></span>

<span data-ttu-id="ae573-110">Este script crea una aplicación de Azure Function App mediante un [plan de App Service](../functions-scale.md#app-service-plan) dedicado.</span><span class="sxs-lookup"><span data-stu-id="ae573-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

<span data-ttu-id="ae573-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Creación de una función de Azure en un plan de App Service")]</span><span class="sxs-lookup"><span data-stu-id="ae573-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ae573-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="ae573-112">Script explanation</span></span>

<span data-ttu-id="ae573-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="ae573-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="ae573-114">Este script usa los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ae573-114">This script uses the following commands:</span></span>

| <span data-ttu-id="ae573-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ae573-115">Command</span></span> | <span data-ttu-id="ae573-116">Notas</span><span class="sxs-lookup"><span data-stu-id="ae573-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ae573-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ae573-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ae573-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="ae573-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ae573-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="ae573-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="ae573-120">Crea una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ae573-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="ae573-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ae573-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="ae573-122">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="ae573-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ae573-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="ae573-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="ae573-124">Crea una instancia de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="ae573-124">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae573-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ae573-125">Next steps</span></span>

<span data-ttu-id="ae573-126">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae573-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ae573-127">Encontrará más ejemplos de scripts de CLI para Azure Functions en la [documentación de Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ae573-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
