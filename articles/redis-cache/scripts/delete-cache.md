---
title: "Ejemplo de script de CLI de Azure: Eliminación de Azure Redis Cache | Microsoft Docs"
description: "Ejemplo de script de CLI de Azure: Eliminación de Azure Redis Cache"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="99682-103">Eliminación de una instancia de Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="99682-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="99682-104">En este escenario, aprenderá a eliminar una instancia de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="99682-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="99682-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="99682-105">Sample script</span></span>

<span data-ttu-id="99682-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span><span class="sxs-lookup"><span data-stu-id="99682-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="99682-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="99682-107">Script explanation</span></span>

<span data-ttu-id="99682-108">Este script usa los siguientes comandos para eliminar una instancia de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="99682-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="99682-109">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="99682-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="99682-110">Comando</span><span class="sxs-lookup"><span data-stu-id="99682-110">Command</span></span> | <span data-ttu-id="99682-111">Notas</span><span class="sxs-lookup"><span data-stu-id="99682-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="99682-112">eliminación de az redis</span><span class="sxs-lookup"><span data-stu-id="99682-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="99682-113">Elimine una instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="99682-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="99682-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99682-114">Next steps</span></span>

<span data-ttu-id="99682-115">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="99682-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="99682-116">Encontrará más ejemplos de scripts de CLI de Azure Redis Cache en la [documentación de Azure Redis Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="99682-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>