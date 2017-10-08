---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una aplicación web de ASP.NET Core en un contenedor de Docker desde el registro de contenedor de Azure | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web ASP.NET Core en un contenedor de Docker desde Azure Container Registry"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 0d4b1e706c2401ef813f48ef4de3d17fa2b6c9e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="10fad-103">Creación de una aplicación web de ASP.NET Core en un contenedor de Docker desde Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="10fad-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="10fad-104">En este escenario, aprenderá cómo toocreate un grupo de recursos, aplicación de Linux plan y la aplicación web de servicio e implementar una aplicación de ASP.NET Core con un contenedor de Docker de hello del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="10fad-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from hello Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="10fad-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="10fad-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="10fad-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="10fad-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="10fad-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10fad-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="10fad-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="10fad-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="10fad-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="10fad-109">Script explanation</span></span>

<span data-ttu-id="10fad-110">Este script utiliza Hola siguientes comandos toocreate un grupo de recursos, aplicación web y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="10fad-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="10fad-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="10fad-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="10fad-112">Comando</span><span class="sxs-lookup"><span data-stu-id="10fad-112">Command</span></span> | <span data-ttu-id="10fad-113">Notas</span><span class="sxs-lookup"><span data-stu-id="10fad-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="10fad-114">az group create</span><span class="sxs-lookup"><span data-stu-id="10fad-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="10fad-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="10fad-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="10fad-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="10fad-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="10fad-117">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="10fad-117">Creates an App Service plan.</span></span> <span data-ttu-id="10fad-118">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="10fad-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="10fad-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="10fad-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="10fad-120">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="10fad-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="10fad-121">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="10fad-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="10fad-122">Establece el contenedor de Docker de hello para la aplicación web de Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="10fad-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="10fad-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10fad-123">Next steps</span></span>

<span data-ttu-id="10fad-124">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="10fad-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="10fad-125">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="10fad-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
