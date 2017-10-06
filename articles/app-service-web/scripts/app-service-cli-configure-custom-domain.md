---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure asignar una aplicación web de tooa de dominio personalizado | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - mapa de una aplicación web de tooa de dominio personalizado"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="2217d-103">Asignar una aplicación web de tooa de dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="2217d-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="2217d-104">Este script de ejemplo crea una aplicación web en el servicio de aplicaciones con sus recursos relacionados y, a continuación, asigna `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="2217d-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2217d-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2217d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2217d-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2217d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2217d-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2217d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2217d-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2217d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2217d-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2217d-109">Script explanation</span></span>

<span data-ttu-id="2217d-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="2217d-110">This script uses hello following commands.</span></span> <span data-ttu-id="2217d-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="2217d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2217d-112">Comando</span><span class="sxs-lookup"><span data-stu-id="2217d-112">Command</span></span> | <span data-ttu-id="2217d-113">Notas</span><span class="sxs-lookup"><span data-stu-id="2217d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2217d-114">az group create</span><span class="sxs-lookup"><span data-stu-id="2217d-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2217d-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="2217d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2217d-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="2217d-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2217d-117">Crea un plan de App Service,</span><span class="sxs-lookup"><span data-stu-id="2217d-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2217d-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="2217d-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="2217d-119">Crea una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2217d-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="2217d-120">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="2217d-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="2217d-121">Asigna una aplicación web de tooa de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="2217d-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2217d-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2217d-122">Next steps</span></span>

<span data-ttu-id="2217d-123">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2217d-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2217d-124">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2217d-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
