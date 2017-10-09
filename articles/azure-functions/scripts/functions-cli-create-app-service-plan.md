---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una aplicación de la función en un plan de servicio de aplicaciones | Documentos de Microsoft"
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
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="62ecc-103">Creación de una instancia de Function App en un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="62ecc-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="62ecc-104">Este script de ejemplo crea una instancia de Azure Function App, que es un contenedor para las funciones.</span><span class="sxs-lookup"><span data-stu-id="62ecc-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="62ecc-105">Hola función aplicación se crea con un plan de servicio de aplicaciones dedicado, lo que significa que los recursos del servidor están siempre activados.</span><span class="sxs-lookup"><span data-stu-id="62ecc-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="62ecc-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="62ecc-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="62ecc-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="62ecc-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="62ecc-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62ecc-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="62ecc-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="62ecc-109">Sample script</span></span>

<span data-ttu-id="62ecc-110">Este script crea una aplicación de Azure Function App mediante un [plan de App Service](../functions-scale.md#app-service-plan) dedicado.</span><span class="sxs-lookup"><span data-stu-id="62ecc-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="62ecc-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="62ecc-111">Script explanation</span></span>

<span data-ttu-id="62ecc-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="62ecc-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="62ecc-113">Este script utiliza Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="62ecc-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="62ecc-114">Comando</span><span class="sxs-lookup"><span data-stu-id="62ecc-114">Command</span></span> | <span data-ttu-id="62ecc-115">Notas</span><span class="sxs-lookup"><span data-stu-id="62ecc-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="62ecc-116">az group create</span><span class="sxs-lookup"><span data-stu-id="62ecc-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="62ecc-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="62ecc-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="62ecc-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="62ecc-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="62ecc-119">Crea una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="62ecc-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="62ecc-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="62ecc-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="62ecc-121">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="62ecc-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="62ecc-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="62ecc-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="62ecc-123">Crea una instancia de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="62ecc-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62ecc-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="62ecc-124">Next steps</span></span>

<span data-ttu-id="62ecc-125">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62ecc-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="62ecc-126">Encontrará más ejemplos de secuencias de comandos de CLI de funciones de Azure en hello [documentación sobre las funciones de Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="62ecc-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
