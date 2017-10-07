---
title: "grupo elástico de aaaCLI ejemplo move SQL de Azure SQL de la base de datos | Documentos de Microsoft"
description: "Azure CLI ejemplo script toomove una base de datos SQL en un grupo elástico de SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="43f61-103">Utilice CLI toomove una base de datos de SQL Azure en un grupo elástico de SQL</span><span class="sxs-lookup"><span data-stu-id="43f61-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="43f61-104">En este ejemplo de secuencia de comandos de CLI de Azure crea dos grupos elásticos, mueve una base de datos de SQL Azure desde un grupo elástico de SQL a otro grupo elástico de SQL y, a continuación, sale de base de datos de hello nivel de rendimiento de grupo elástico tooa única base de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="43f61-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="43f61-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="43f61-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="43f61-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="43f61-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="43f61-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="43f61-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="43f61-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="43f61-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="43f61-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="43f61-109">Clean up deployment</span></span>

<span data-ttu-id="43f61-110">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="43f61-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="43f61-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="43f61-111">Script explanation</span></span>

<span data-ttu-id="43f61-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="43f61-112">This script uses hello following commands.</span></span> <span data-ttu-id="43f61-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="43f61-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="43f61-114">Comando</span><span class="sxs-lookup"><span data-stu-id="43f61-114">Command</span></span> | <span data-ttu-id="43f61-115">Notas</span><span class="sxs-lookup"><span data-stu-id="43f61-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="43f61-116">az group create</span><span class="sxs-lookup"><span data-stu-id="43f61-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="43f61-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="43f61-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="43f61-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="43f61-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="43f61-119">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="43f61-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="43f61-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="43f61-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="43f61-121">Crea un grupo elástico en el servidor lógico Hola.</span><span class="sxs-lookup"><span data-stu-id="43f61-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="43f61-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="43f61-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="43f61-123">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="43f61-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="43f61-124">az sql db update</span><span class="sxs-lookup"><span data-stu-id="43f61-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="43f61-125">Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="43f61-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="43f61-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="43f61-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="43f61-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="43f61-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43f61-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43f61-128">Next steps</span></span>

<span data-ttu-id="43f61-129">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43f61-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="43f61-130">Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de SQL en hello [documentación de la base de datos de SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="43f61-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


