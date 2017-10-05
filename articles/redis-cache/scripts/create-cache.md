---
title: "Ejemplo de script de CLI de Azure: creación de Azure Redis Cache | Microsoft Docs"
description: "Ejemplo de script de CLI de Azure: creación de Azure Redis Cache"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="65614-103">Creación de una instancia de Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="65614-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="65614-104">En este escenario, aprenderá a crear una instancia de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="65614-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="65614-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65614-105">Sample script</span></span>

<span data-ttu-id="65614-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="65614-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="65614-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="65614-107">Script explanation</span></span>

<span data-ttu-id="65614-108">Este script usa los siguientes comandos para crear un grupo de recursos y una instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="65614-108">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="65614-109">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="65614-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="65614-110">Comando</span><span class="sxs-lookup"><span data-stu-id="65614-110">Command</span></span> | <span data-ttu-id="65614-111">Notas</span><span class="sxs-lookup"><span data-stu-id="65614-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="65614-112">az group create</span><span class="sxs-lookup"><span data-stu-id="65614-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="65614-113">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="65614-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="65614-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="65614-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="65614-115">Crea una instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="65614-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="65614-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65614-116">Next steps</span></span>

<span data-ttu-id="65614-117">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65614-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="65614-118">Encontrará más ejemplos de scripts de CLI de Azure Redis Cache en la [documentación de Azure Redis Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="65614-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>