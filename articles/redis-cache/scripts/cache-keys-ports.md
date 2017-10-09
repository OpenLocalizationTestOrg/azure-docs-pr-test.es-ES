---
title: "Ejemplo de secuencia de comandos de CLI - Get hello hostname, puertos y las claves de caché en Redis de Azure aaaAzure | Documentos de Microsoft"
description: "Azure ejemplo de secuencia de comandos CLI - Get hello hostname, puertos y las claves para una instancia de caché en Redis de Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="f9797-103">Obtener Hola hostname, puertos y las claves de caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="f9797-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="f9797-104">En este escenario, aprenderá cómo claves, puertos y el nombre de host de tooretrieve Hola utilizan la instancia de caché en Redis de Azure de tooconnect tooan.</span><span class="sxs-lookup"><span data-stu-id="f9797-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f9797-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f9797-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="f9797-106">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f9797-106">Script explanation</span></span>

<span data-ttu-id="f9797-107">Este script utiliza Hola después el nombre de host de comandos tooretrieve hello, claves y los puertos de una instancia de caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="f9797-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="f9797-108">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="f9797-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f9797-109">Comando</span><span class="sxs-lookup"><span data-stu-id="f9797-109">Command</span></span> | <span data-ttu-id="f9797-110">Notas</span><span class="sxs-lookup"><span data-stu-id="f9797-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f9797-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="f9797-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="f9797-112">Recupera detalles de una instancia de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="f9797-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="f9797-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="f9797-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="f9797-114">Recupera las claves de acceso para una instancia de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="f9797-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f9797-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9797-115">Next steps</span></span>

<span data-ttu-id="f9797-116">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f9797-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f9797-117">Encontrará más ejemplos de secuencias de comandos de CLI de caché de Redis de Azure en hello [documentación de Azure Redis Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f9797-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
