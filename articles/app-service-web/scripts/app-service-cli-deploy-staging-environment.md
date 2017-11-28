---
title: "aaaAzure ejemplo de secuencia de comandos de CLI: crear una aplicación web e implementar el entorno de ensayo de tooa de código | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - crear una aplicación web e implementar el entorno de ensayo de tooa de código"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="0871b-103">Crear una aplicación web e implementar el entorno de ensayo de tooa de código</span><span class="sxs-lookup"><span data-stu-id="0871b-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="0871b-104">Este script de ejemplo crea una aplicación web en el servicio de aplicaciones con una ranura de implementación adicionales que se denomina "ensayo" y, a continuación, implementa una toohello de aplicación de ejemplo "ensayo" ranura.</span><span class="sxs-lookup"><span data-stu-id="0871b-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0871b-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0871b-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0871b-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="0871b-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0871b-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0871b-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0871b-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0871b-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0871b-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0871b-109">Script explanation</span></span>

<span data-ttu-id="0871b-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="0871b-110">This script uses hello following commands.</span></span> <span data-ttu-id="0871b-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="0871b-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0871b-112">Comando</span><span class="sxs-lookup"><span data-stu-id="0871b-112">Command</span></span> | <span data-ttu-id="0871b-113">Notas</span><span class="sxs-lookup"><span data-stu-id="0871b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0871b-114">az group create</span><span class="sxs-lookup"><span data-stu-id="0871b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0871b-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0871b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0871b-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="0871b-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0871b-117">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="0871b-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0871b-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="0871b-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0871b-119">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="0871b-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0871b-120">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="0871b-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="0871b-121">Crea una ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="0871b-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="0871b-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="0871b-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="0871b-123">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="0871b-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="0871b-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="0871b-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="0871b-125">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="0871b-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="0871b-126">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="0871b-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="0871b-127">Cambia la ranura de implementación especificada a producción.</span><span class="sxs-lookup"><span data-stu-id="0871b-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0871b-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0871b-128">Next steps</span></span>

<span data-ttu-id="0871b-129">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0871b-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0871b-130">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0871b-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
