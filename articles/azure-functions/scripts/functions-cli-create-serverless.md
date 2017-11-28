---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una aplicación de función para la ejecución sin servidor | Documentos de Microsoft"
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="3c53c-103">Creación de una instancia de Function App para la ejecución sin servidor</span><span class="sxs-lookup"><span data-stu-id="3c53c-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="3c53c-104">Este script de ejemplo crea una instancia de Azure Function App, que es un contenedor para las funciones.</span><span class="sxs-lookup"><span data-stu-id="3c53c-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="3c53c-105">Hello función aplicación se crea utilizando hello [plan de consumo](../functions-scale.md#consumption-plan), lo que es ideal para las cargas de trabajo sin servidor orientada a eventos.</span><span class="sxs-lookup"><span data-stu-id="3c53c-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3c53c-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="3c53c-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3c53c-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c53c-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3c53c-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3c53c-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3c53c-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3c53c-109">Sample script</span></span>

<span data-ttu-id="3c53c-110">Este script crea una aplicación de función de Azure con hello [plan de consumo](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="3c53c-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3c53c-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="3c53c-111">Script explanation</span></span>

<span data-ttu-id="3c53c-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="3c53c-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="3c53c-113">Este script utiliza Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3c53c-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="3c53c-114">Comando</span><span class="sxs-lookup"><span data-stu-id="3c53c-114">Command</span></span> | <span data-ttu-id="3c53c-115">Notas</span><span class="sxs-lookup"><span data-stu-id="3c53c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3c53c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="3c53c-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3c53c-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="3c53c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3c53c-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="3c53c-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="3c53c-119">Crea una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3c53c-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="3c53c-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="3c53c-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="3c53c-121">Crea una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c53c-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3c53c-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c53c-122">Next steps</span></span>

<span data-ttu-id="3c53c-123">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c53c-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3c53c-124">Encontrará más ejemplos de secuencias de comandos de CLI de funciones de Azure en hello [documentación sobre las funciones de Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3c53c-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
