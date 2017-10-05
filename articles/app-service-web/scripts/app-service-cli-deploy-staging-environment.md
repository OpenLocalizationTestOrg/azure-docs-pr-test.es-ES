---
title: "Ejemplo de script de la CLI de Azure: creación de una aplicación web e implementación de código en un entorno de ensayo | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web e implementación de código en un entorno de ensayo"
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
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="bbbbf-103">Creación de una aplicación web e implementación de código en un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="bbbbf-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="bbbbf-104">Este script de ejemplo crea una aplicación web en App Service con una ranura de implementación adicional que se denomina "ensayo" y, a continuación, implementa una aplicación de ejemplo en la ranura "ensayo".</span><span class="sxs-lookup"><span data-stu-id="bbbbf-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bbbbf-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bbbbf-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="bbbbf-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bbbbf-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bbbbf-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bbbbf-108">Sample script</span></span>

<span data-ttu-id="bbbbf-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Creación de una aplicación web e implementación de código en un entorno de ensayo")]</span><span class="sxs-lookup"><span data-stu-id="bbbbf-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bbbbf-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="bbbbf-110">Script explanation</span></span>

<span data-ttu-id="bbbbf-111">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-111">This script uses the following commands.</span></span> <span data-ttu-id="bbbbf-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bbbbf-113">Comando</span><span class="sxs-lookup"><span data-stu-id="bbbbf-113">Command</span></span> | <span data-ttu-id="bbbbf-114">Notas</span><span class="sxs-lookup"><span data-stu-id="bbbbf-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bbbbf-115">az group create</span><span class="sxs-lookup"><span data-stu-id="bbbbf-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bbbbf-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bbbbf-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="bbbbf-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bbbbf-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="bbbbf-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="bbbbf-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="bbbbf-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="bbbbf-120">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="bbbbf-121">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="bbbbf-121">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="bbbbf-122">Crea una ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-122">Create a deployment slot.</span></span> |
| [<span data-ttu-id="bbbbf-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="bbbbf-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="bbbbf-124">Asocia una aplicación web de Azure con un repositorio de GIT o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="bbbbf-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="bbbbf-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="bbbbf-126">Abre una aplicación web de Azure en un explorador.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-126">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="bbbbf-127">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="bbbbf-127">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="bbbbf-128">Cambia la ranura de implementación especificada a producción.</span><span class="sxs-lookup"><span data-stu-id="bbbbf-128">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bbbbf-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bbbbf-129">Next steps</span></span>

<span data-ttu-id="bbbbf-130">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bbbbf-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bbbbf-131">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bbbbf-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
