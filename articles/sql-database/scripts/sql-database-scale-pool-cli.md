---
title: "El ejemplo de la CLI escala un grupo elástico de SQL en Azure SQL Database | Microsoft Docs"
description: "Script de ejemplo de la CLI de Azure para escalar un grupo elástico de SQL en Azure SQL Database"
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
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="16eac-103">Uso de la CLI para escalar un grupo elástico de SQL en Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="16eac-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="16eac-104">Este script de ejemplo de la CLI de Azure crea grupos elásticos de SQL, traslada bases de datos agrupadas y cambia los niveles de rendimiento de los grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="16eac-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="16eac-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="16eac-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="16eac-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="16eac-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="16eac-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="16eac-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="16eac-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="16eac-108">Sample script</span></span>

<span data-ttu-id="16eac-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Traslado de una base de datos de un grupo a otro")]</span><span class="sxs-lookup"><span data-stu-id="16eac-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="16eac-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="16eac-110">Clean up deployment</span></span>

<span data-ttu-id="16eac-111">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="16eac-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="16eac-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="16eac-112">Script explanation</span></span>

<span data-ttu-id="16eac-113">Este script usa los siguientes comandos para crear un grupo de recursos, un servidor lógico, una base de datos SQL y reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="16eac-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="16eac-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="16eac-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="16eac-115">Comando</span><span class="sxs-lookup"><span data-stu-id="16eac-115">Command</span></span> | <span data-ttu-id="16eac-116">Notas</span><span class="sxs-lookup"><span data-stu-id="16eac-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16eac-117">az group create</span><span class="sxs-lookup"><span data-stu-id="16eac-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="16eac-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="16eac-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="16eac-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="16eac-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="16eac-120">Crea un servidor lógico que hospeda la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="16eac-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="16eac-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="16eac-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="16eac-122">Crea un grupo elástico de bases de datos en el servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="16eac-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="16eac-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="16eac-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="16eac-124">Crea una base de datos SQL en el servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="16eac-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="16eac-125">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="16eac-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="16eac-126">Actualiza un grupo elástico de bases de datos; en este ejemplo, cambia la eDTU asignada.</span><span class="sxs-lookup"><span data-stu-id="16eac-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="16eac-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="16eac-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="16eac-128">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="16eac-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="16eac-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16eac-129">Next steps</span></span>

<span data-ttu-id="16eac-130">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="16eac-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="16eac-131">Encontrará más ejemplos de scripts de la CLI de SQL Database en la [documentación de Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="16eac-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
