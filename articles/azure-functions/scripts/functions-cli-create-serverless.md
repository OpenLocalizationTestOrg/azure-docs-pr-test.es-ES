---
title: "Ejemplo de script de la CLI de Azure: creación de una instancia de Function App para la ejecución sin servidor | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una instancia de Function App para la ejecución sin servidor"
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
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="4bf2a-103">Creación de una instancia de Function App para la ejecución sin servidor</span><span class="sxs-lookup"><span data-stu-id="4bf2a-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="4bf2a-104">Este script de ejemplo crea una instancia de Azure Function App, que es un contenedor para las funciones.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="4bf2a-105">La instancia de Function App se creará usando el [plan de consumo](../functions-scale.md#consumption-plan), que es ideal para las cargas de trabajo sin servidor controladas por eventos.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-105">The Function App is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4bf2a-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4bf2a-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="4bf2a-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4bf2a-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4bf2a-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4bf2a-109">Sample script</span></span>

<span data-ttu-id="4bf2a-110">Este script crea una aplicación de Azure Function App con el [plan de consumo](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="4bf2a-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

<span data-ttu-id="4bf2a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Creación de una función de Azure en un plan de consumo")]</span><span class="sxs-lookup"><span data-stu-id="4bf2a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4bf2a-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="4bf2a-112">Script explanation</span></span>

<span data-ttu-id="4bf2a-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="4bf2a-114">Este script usa los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4bf2a-114">This script uses the following commands:</span></span>

| <span data-ttu-id="4bf2a-115">Comando</span><span class="sxs-lookup"><span data-stu-id="4bf2a-115">Command</span></span> | <span data-ttu-id="4bf2a-116">Notas</span><span class="sxs-lookup"><span data-stu-id="4bf2a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4bf2a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="4bf2a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4bf2a-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4bf2a-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="4bf2a-119">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="4bf2a-120">Crea una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="4bf2a-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="4bf2a-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="4bf2a-122">Crea una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf2a-122">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4bf2a-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4bf2a-123">Next steps</span></span>

<span data-ttu-id="4bf2a-124">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4bf2a-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4bf2a-125">Encontrará más ejemplos de scripts de CLI para Azure Functions en la [documentación de Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4bf2a-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
