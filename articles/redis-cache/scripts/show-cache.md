---
title: 'Ejemplo de script de CLI de Azure: detalles sobre Azure Redis Cache | Microsoft Docs'
description: 'Ejemplo de script de CLI de Azure: detalles sobre Azure Redis Cache'
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="585ff-103">Obtenga detalles sobre una instancia de Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="585ff-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="585ff-104">En este escenario, obtendrá información sobre cómo recuperar los detalles de una instancia de Azure Redis Cache, incluido su estado de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="585ff-104">In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="585ff-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="585ff-105">Sample script</span></span>

<span data-ttu-id="585ff-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="585ff-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="585ff-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="585ff-107">Script explanation</span></span>

<span data-ttu-id="585ff-108">Este script usa los comandos siguientes para recuperar los detalles de una instancia de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="585ff-108">This script uses the following commands to retrieve the details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="585ff-109">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="585ff-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="585ff-110">Comando</span><span class="sxs-lookup"><span data-stu-id="585ff-110">Command</span></span> | <span data-ttu-id="585ff-111">Notas</span><span class="sxs-lookup"><span data-stu-id="585ff-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="585ff-112">az redis show</span><span class="sxs-lookup"><span data-stu-id="585ff-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="585ff-113">Recupera detalles de una instancia de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="585ff-113">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="585ff-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="585ff-114">Next steps</span></span>

<span data-ttu-id="585ff-115">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="585ff-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="585ff-116">Encontrará más ejemplos de scripts de CLI de Azure Redis Cache en la [documentación de Azure Redis Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="585ff-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>