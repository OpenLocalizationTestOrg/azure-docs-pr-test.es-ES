---
title: "Ejemplo de script de CLI de Azure: creación de Azure Redis Cache premium con agrupación en clústeres | Microsoft Docs"
description: "Ejemplo de script de CLI de Azure: Creación de Azure Redis Cache de nivel premium con agrupación en clústeres"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="1421d-103">Creación de una caché en Azure Redis Cache premium con agrupación en clústeres</span><span class="sxs-lookup"><span data-stu-id="1421d-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="1421d-104">En este escenario, aprenderá cómo crear Azure Redis Cache de nivel Premium de 6 GB con la agrupación en clústeres habilitada y dos particiones.</span><span class="sxs-lookup"><span data-stu-id="1421d-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="1421d-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1421d-105">Sample script</span></span>

<span data-ttu-id="1421d-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="1421d-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1421d-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="1421d-107">Script explanation</span></span>

<span data-ttu-id="1421d-108">Este script usa los siguientes comandos para crear un grupo de recursos y una caché en Redis de nivel premium con la habilitación de agrupación en clústeres.</span><span class="sxs-lookup"><span data-stu-id="1421d-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="1421d-109">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="1421d-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1421d-110">Comando</span><span class="sxs-lookup"><span data-stu-id="1421d-110">Command</span></span> | <span data-ttu-id="1421d-111">Notas</span><span class="sxs-lookup"><span data-stu-id="1421d-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1421d-112">az group create</span><span class="sxs-lookup"><span data-stu-id="1421d-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1421d-113">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="1421d-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1421d-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="1421d-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="1421d-115">Crea una instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="1421d-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1421d-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1421d-116">Next steps</span></span>

<span data-ttu-id="1421d-117">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1421d-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1421d-118">Encontrará más ejemplos de scripts de CLI de Azure Redis Cache en la [documentación de Azure Redis Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1421d-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>