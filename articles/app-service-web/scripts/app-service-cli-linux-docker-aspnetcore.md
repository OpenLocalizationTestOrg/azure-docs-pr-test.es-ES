---
title: "Ejemplo de script de la CLI de Azure: creación de una aplicación web ASP.NET Core en un contenedor de Docker | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una aplicación web ASP.NET Core en un contenedor de Docker"
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
ms.openlocfilehash: 5d1e2c7d2815df5fb9c176ec290a18d330ea3f7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="6ff83-103">Creación de una aplicación web de ASP.NET Core en un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="6ff83-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="6ff83-104">En este escenario aprenderá cómo crear un grupo de recursos, el plan de servicio de aplicaciones de Linux y la aplicación web, y cómo implementar una aplicación de ASP.NET Core utilizando un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="6ff83-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6ff83-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="6ff83-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6ff83-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="6ff83-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6ff83-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6ff83-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="6ff83-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6ff83-108">Sample script</span></span>

<span data-ttu-id="6ff83-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]</span><span class="sxs-lookup"><span data-stu-id="6ff83-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6ff83-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6ff83-110">Script explanation</span></span>

<span data-ttu-id="6ff83-111">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6ff83-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="6ff83-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="6ff83-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6ff83-113">Comando</span><span class="sxs-lookup"><span data-stu-id="6ff83-113">Command</span></span> | <span data-ttu-id="6ff83-114">Notas</span><span class="sxs-lookup"><span data-stu-id="6ff83-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ff83-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6ff83-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6ff83-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6ff83-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ff83-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6ff83-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6ff83-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="6ff83-118">Creates an App Service plan.</span></span> <span data-ttu-id="6ff83-119">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff83-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6ff83-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6ff83-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6ff83-121">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff83-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6ff83-122">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="6ff83-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="6ff83-123">Establece el contenedor de Docker para la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff83-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ff83-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ff83-124">Next steps</span></span>

<span data-ttu-id="6ff83-125">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ff83-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6ff83-126">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6ff83-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
