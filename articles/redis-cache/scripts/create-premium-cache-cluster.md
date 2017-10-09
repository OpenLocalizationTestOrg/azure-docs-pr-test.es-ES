---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una caché en Redis de Azure Premium con los clústeres de | Documentos de Microsoft"
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
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="f5eb8-103">Creación de una caché en Azure Redis Cache premium con agrupación en clústeres</span><span class="sxs-lookup"><span data-stu-id="f5eb8-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="f5eb8-104">En este escenario, aprenderá cómo toocreate un nivel Premium de 6 GB caché en Redis de Azure con los clústeres habilitado y dos particiones.</span><span class="sxs-lookup"><span data-stu-id="f5eb8-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f5eb8-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f5eb8-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f5eb8-106">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f5eb8-106">Script explanation</span></span>

<span data-ttu-id="f5eb8-107">Este script utiliza Hola después comandos toocreate un grupo de recursos y una caché en redis nivel Premium con agrupación en clústeres habilitar.</span><span class="sxs-lookup"><span data-stu-id="f5eb8-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="f5eb8-108">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="f5eb8-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f5eb8-109">Comando</span><span class="sxs-lookup"><span data-stu-id="f5eb8-109">Command</span></span> | <span data-ttu-id="f5eb8-110">Notas</span><span class="sxs-lookup"><span data-stu-id="f5eb8-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f5eb8-111">az group create</span><span class="sxs-lookup"><span data-stu-id="f5eb8-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f5eb8-112">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f5eb8-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f5eb8-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="f5eb8-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="f5eb8-114">Crea una instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="f5eb8-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f5eb8-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5eb8-115">Next steps</span></span>

<span data-ttu-id="f5eb8-116">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5eb8-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f5eb8-117">Encontrará más ejemplos de secuencias de comandos de CLI de caché de Redis de Azure en hello [documentación de Azure Redis Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f5eb8-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
