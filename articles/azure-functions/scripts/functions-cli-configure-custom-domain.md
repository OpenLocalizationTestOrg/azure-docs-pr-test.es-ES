---
title: "Ejemplo de script de la CLI de Azure: asignación de un dominio personalizado a una aplicación de función | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: asignación de un dominio personalizado a una aplicación de función en Azure."
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
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="f047f-103">Asignación de un dominio personalizado a una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="f047f-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="f047f-104">Este script de ejemplo crea una aplicación de función con recursos relacionados y le asigna `www.<yourdomain>`.</span><span class="sxs-lookup"><span data-stu-id="f047f-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="f047f-105">Para asignarla a un dominio personalizado, la aplicación de función se debe crear en un plan de App Service y no en un plan de consumo.</span><span class="sxs-lookup"><span data-stu-id="f047f-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="f047f-106">Azure Functions solo admite la asignación de un dominio personalizado mediante un registro D.</span><span class="sxs-lookup"><span data-stu-id="f047f-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f047f-107">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f047f-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f047f-108">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="f047f-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="f047f-109">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f047f-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="f047f-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f047f-110">Sample script</span></span>

<span data-ttu-id="f047f-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Asignación de un dominio personalizado a una aplicación de función")]</span><span class="sxs-lookup"><span data-stu-id="f047f-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f047f-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f047f-112">Script explanation</span></span>

<span data-ttu-id="f047f-113">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="f047f-113">This script uses the following commands.</span></span> <span data-ttu-id="f047f-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="f047f-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f047f-115">Comando</span><span class="sxs-lookup"><span data-stu-id="f047f-115">Command</span></span> | <span data-ttu-id="f047f-116">Notas</span><span class="sxs-lookup"><span data-stu-id="f047f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f047f-117">az group create</span><span class="sxs-lookup"><span data-stu-id="f047f-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f047f-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f047f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f047f-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="f047f-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="f047f-120">Crea una cuenta de almacenamiento necesaria para la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="f047f-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="f047f-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f047f-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f047f-122">Crea un plan de App Service necesario para asignar un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="f047f-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="f047f-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="f047f-123">az functionapp create</span></span>]() | <span data-ttu-id="f047f-124">Crea una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="f047f-124">Creates a function app.</span></span> |
| [<span data-ttu-id="f047f-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="f047f-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="f047f-126">Asigna un dominio personalizado a una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="f047f-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f047f-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f047f-127">Next steps</span></span>

<span data-ttu-id="f047f-128">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f047f-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f047f-129">Encontrará más ejemplos de scripts de CLI para Functions en la [documentación de Azure Functions]().</span><span class="sxs-lookup"><span data-stu-id="f047f-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
