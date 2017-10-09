---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure asignar una aplicación de función de dominio personalizado tooa | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos para Azure CLI - mapa de una aplicación de función de dominio personalizado tooa en Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="db33f-103">Asignar una aplicación de función de dominio personalizado tooa</span><span class="sxs-lookup"><span data-stu-id="db33f-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="db33f-104">Este script de ejemplo crea una aplicación de la función con recursos relacionados y, a continuación, asigna `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="db33f-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="db33f-105">dominio personalizado de toomap tooa, la aplicación de la función debe crearse en un plan de servicio de aplicaciones y no en un plan de consumo.</span><span class="sxs-lookup"><span data-stu-id="db33f-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="db33f-106">Azure Functions solo admite la asignación de un dominio personalizado mediante un registro D.</span><span class="sxs-lookup"><span data-stu-id="db33f-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="db33f-107">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="db33f-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="db33f-108">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="db33f-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="db33f-109">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="db33f-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="db33f-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="db33f-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="db33f-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="db33f-111">Script explanation</span></span>

<span data-ttu-id="db33f-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="db33f-112">This script uses hello following commands.</span></span> <span data-ttu-id="db33f-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="db33f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="db33f-114">Comando</span><span class="sxs-lookup"><span data-stu-id="db33f-114">Command</span></span> | <span data-ttu-id="db33f-115">Notas</span><span class="sxs-lookup"><span data-stu-id="db33f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="db33f-116">az group create</span><span class="sxs-lookup"><span data-stu-id="db33f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="db33f-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="db33f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="db33f-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="db33f-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="db33f-119">Crea una cuenta de almacenamiento necesaria para la aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="db33f-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="db33f-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="db33f-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="db33f-121">Crea un toomap requerido un plan de servicio de aplicaciones en un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="db33f-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="db33f-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="db33f-122">az functionapp create</span></span>]() | <span data-ttu-id="db33f-123">Crea una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="db33f-123">Creates a function app.</span></span> |
| [<span data-ttu-id="db33f-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="db33f-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="db33f-125">Asigna una aplicación de función de tooa de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="db33f-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="db33f-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db33f-126">Next steps</span></span>

<span data-ttu-id="db33f-127">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="db33f-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="db33f-128">Encontrará más ejemplos de secuencias de comandos de CLI de funciones en hello [documentación sobre las funciones de Azure]().</span><span class="sxs-lookup"><span data-stu-id="db33f-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
