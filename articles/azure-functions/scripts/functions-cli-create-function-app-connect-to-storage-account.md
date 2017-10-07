---
title: "aaaCreate una función de Azure que se conecta tooan almacenamiento de Azure | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: crear una función de Azure que se conecta tooan almacenamiento de Azure"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="5f0f9-103">Integración de Function App en una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5f0f9-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="5f0f9-104">Este script de ejemplo crea una instancia de Function App y una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5f0f9-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5f0f9-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5f0f9-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5f0f9-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5f0f9-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5f0f9-108">Sample script</span></span>

<span data-ttu-id="5f0f9-109">Este ejemplo crea una aplicación de la función de Azure y agrega la configuración de la aplicación hello almacenamiento conexión cadena tooan.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="5f0f9-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5f0f9-110">Clean up deployment</span></span>

<span data-ttu-id="5f0f9-111">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación de servicio de aplicaciones y recursos de todos ellos relacionados con:</span><span class="sxs-lookup"><span data-stu-id="5f0f9-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5f0f9-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5f0f9-112">Script explanation</span></span>

<span data-ttu-id="5f0f9-113">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-113">This script uses hello following commands.</span></span> <span data-ttu-id="5f0f9-114">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5f0f9-115">Comando</span><span class="sxs-lookup"><span data-stu-id="5f0f9-115">Command</span></span> | <span data-ttu-id="5f0f9-116">Notas</span><span class="sxs-lookup"><span data-stu-id="5f0f9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f0f9-117">az login</span><span class="sxs-lookup"><span data-stu-id="5f0f9-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="5f0f9-118">TooAzure de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="5f0f9-119">az group create</span><span class="sxs-lookup"><span data-stu-id="5f0f9-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5f0f9-120">Crea un grupo de recursos con una ubicación.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="5f0f9-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="5f0f9-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="5f0f9-122">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5f0f9-122">Create a storage account</span></span> |
| [<span data-ttu-id="5f0f9-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="5f0f9-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="5f0f9-124">Crea una nueva instancia de Function App.</span><span class="sxs-lookup"><span data-stu-id="5f0f9-124">Create a new function app</span></span> |
| [<span data-ttu-id="5f0f9-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="5f0f9-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="5f0f9-126">Limpieza</span><span class="sxs-lookup"><span data-stu-id="5f0f9-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f0f9-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f0f9-127">Next steps</span></span>

<span data-ttu-id="5f0f9-128">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f0f9-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5f0f9-129">Encontrará más ejemplos de secuencias de comandos de CLI de funciones de Azure en hello [documentación sobre las funciones de Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5f0f9-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
