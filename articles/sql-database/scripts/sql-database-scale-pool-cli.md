---
title: "en el ejemplo aaaCLI se escala una base de datos SQL de Azure de grupo elástico de SQL | Documentos de Microsoft"
description: "Azure CLI ejemplo script tooscale un grupo elástico de SQL en la base de datos de SQL Azure"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="8c3e9-103">Utilice CLI tooscale un grupo elástico de SQL en la base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8c3e9-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="8c3e9-104">Este script de ejemplo de la CLI de Azure crea grupos elásticos de SQL, traslada bases de datos agrupadas y cambia los niveles de rendimiento de los grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8c3e9-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8c3e9-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8c3e9-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8c3e9-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8c3e9-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c3e9-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8c3e9-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="8c3e9-109">Clean up deployment</span></span>

<span data-ttu-id="8c3e9-110">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8c3e9-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="8c3e9-111">Script explanation</span></span>

<span data-ttu-id="8c3e9-112">Este script utiliza Hola después comandos toocreate un grupo de recursos, servidor lógico, base de datos SQL y las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="8c3e9-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8c3e9-114">Comando</span><span class="sxs-lookup"><span data-stu-id="8c3e9-114">Command</span></span> | <span data-ttu-id="8c3e9-115">Notas</span><span class="sxs-lookup"><span data-stu-id="8c3e9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8c3e9-116">az group create</span><span class="sxs-lookup"><span data-stu-id="8c3e9-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8c3e9-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8c3e9-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="8c3e9-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="8c3e9-119">Crea un servidor lógico que hospeda Hola base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="8c3e9-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="8c3e9-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="8c3e9-121">Crea un grupo elástico de base de datos en el servidor lógico Hola.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="8c3e9-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="8c3e9-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="8c3e9-123">Crea Hola base de datos SQL en el servidor lógico Hola.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="8c3e9-124">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="8c3e9-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="8c3e9-125">Actualiza un grupo elástico de base de datos, en este Hola de cambios en el ejemplo se asignan eDTU.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="8c3e9-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="8c3e9-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="8c3e9-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="8c3e9-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8c3e9-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c3e9-128">Next steps</span></span>

<span data-ttu-id="8c3e9-129">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8c3e9-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8c3e9-130">Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de SQL en hello [documentación de la base de datos de SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8c3e9-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
