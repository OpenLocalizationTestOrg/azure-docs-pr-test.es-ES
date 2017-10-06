---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure escalar una aplicación web en todo el mundo con una arquitectura de alta disponibilidad | Documentos de Microsoft"
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
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="4a223-103">Escalado de una aplicación web en todo el mundo con una arquitectura de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="4a223-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="4a223-104">En este escenario, creará un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="4a223-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="4a223-105">Cuando se complete el ejercicio de hello tendrá una alta disponibilidad arquitectura que permite que proporciona disponibilidad global de la aplicación web en función de la latencia de red más baja de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a223-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4a223-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4a223-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4a223-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a223-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4a223-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4a223-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="4a223-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4a223-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4a223-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="4a223-110">Script explanation</span></span>

<span data-ttu-id="4a223-111">Este script utiliza Hola después comandos toocreate un grupo de recursos, la aplicación web, el perfil del Administrador de tráfico y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4a223-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="4a223-112">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="4a223-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4a223-113">Comando</span><span class="sxs-lookup"><span data-stu-id="4a223-113">Command</span></span> | <span data-ttu-id="4a223-114">Notas</span><span class="sxs-lookup"><span data-stu-id="4a223-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4a223-115">az group create</span><span class="sxs-lookup"><span data-stu-id="4a223-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4a223-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="4a223-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4a223-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="4a223-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4a223-118">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="4a223-118">Creates an App Service plan.</span></span> <span data-ttu-id="4a223-119">que es como una granja de servidores para una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a223-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="4a223-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="4a223-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="4a223-121">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a223-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="4a223-122">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="4a223-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="4a223-123">Crea un perfil de Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="4a223-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="4a223-124">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="4a223-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="4a223-125">Agrega un perfil de Traffic Manager de Azure tooan de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="4a223-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4a223-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a223-126">Next steps</span></span>

<span data-ttu-id="4a223-127">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4a223-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4a223-128">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4a223-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
