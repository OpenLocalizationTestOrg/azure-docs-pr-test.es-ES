---
title: "Ejemplo de script de la CLI de Azure: escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="e1d22-103">Escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="e1d22-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="e1d22-104">En este escenario, creará un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e1d22-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="e1d22-105">Una vez completado el ejercicio, tendrá una arquitectura de alta disponibilidad que garantizará la disponibilidad global de la aplicación web en función de la latencia de red más baja.</span><span class="sxs-lookup"><span data-stu-id="e1d22-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e1d22-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e1d22-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e1d22-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="e1d22-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="e1d22-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1d22-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="e1d22-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1d22-109">Sample script</span></span>

<span data-ttu-id="e1d22-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Escalado geográfico")]</span><span class="sxs-lookup"><span data-stu-id="e1d22-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e1d22-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="e1d22-111">Script explanation</span></span>

<span data-ttu-id="e1d22-112">Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web, un perfil de Traffic Manager y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e1d22-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="e1d22-113">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="e1d22-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e1d22-114">Comando</span><span class="sxs-lookup"><span data-stu-id="e1d22-114">Command</span></span> | <span data-ttu-id="e1d22-115">Notas</span><span class="sxs-lookup"><span data-stu-id="e1d22-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e1d22-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e1d22-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e1d22-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="e1d22-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e1d22-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e1d22-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e1d22-119">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="e1d22-119">Creates an App Service plan.</span></span> <span data-ttu-id="e1d22-120">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d22-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e1d22-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e1d22-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e1d22-122">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d22-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e1d22-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="e1d22-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="e1d22-124">Crea un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e1d22-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="e1d22-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="e1d22-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="e1d22-126">Añade un punto de conexión a un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e1d22-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e1d22-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1d22-127">Next steps</span></span>

<span data-ttu-id="e1d22-128">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e1d22-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e1d22-129">Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e1d22-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
