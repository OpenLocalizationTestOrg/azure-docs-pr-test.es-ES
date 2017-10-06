---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una caché en Redis de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="d193d-103">Creación de una instancia de Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="d193d-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="d193d-104">En este escenario, aprenderá cómo toocreate un Redis de Azure almacenan en caché.</span><span class="sxs-lookup"><span data-stu-id="d193d-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="d193d-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d193d-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d193d-106">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d193d-106">Script explanation</span></span>

<span data-ttu-id="d193d-107">Este script utiliza Hola después comandos toocreate un grupo de recursos y una caché de redis.</span><span class="sxs-lookup"><span data-stu-id="d193d-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="d193d-108">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="d193d-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d193d-109">Comando</span><span class="sxs-lookup"><span data-stu-id="d193d-109">Command</span></span> | <span data-ttu-id="d193d-110">Notas</span><span class="sxs-lookup"><span data-stu-id="d193d-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d193d-111">az group create</span><span class="sxs-lookup"><span data-stu-id="d193d-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d193d-112">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d193d-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d193d-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="d193d-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="d193d-114">Crea una instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="d193d-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d193d-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d193d-115">Next steps</span></span>

<span data-ttu-id="d193d-116">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d193d-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d193d-117">Encontrará más ejemplos de secuencias de comandos de CLI de caché de Redis de Azure en hello [documentación de Azure Redis Cache](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d193d-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
