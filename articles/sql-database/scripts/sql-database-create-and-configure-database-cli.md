---
title: 'ejemplo: crear aaaCLI una base de datos SQL de Azure | Documentos de Microsoft'
description: Azure CLI ejemplo script toocreate una base de datos SQL
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="3a285-103">Utilice CLI toocreate una sola base de datos de SQL Azure y configurar una regla de firewall</span><span class="sxs-lookup"><span data-stu-id="3a285-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="3a285-104">Este script de ejemplo de la CLI de Azure crea una instancia de Azure SQL Database y configura una regla de firewall en el nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="3a285-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="3a285-105">Una vez que se ha ejecutado correctamente el script de Hola, base de datos SQL puede tener acceso desde todos los servicios de Azure de Hola y Hola configuran dirección IP.</span><span class="sxs-lookup"><span data-stu-id="3a285-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3a285-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="3a285-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3a285-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a285-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3a285-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3a285-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3a285-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3a285-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3a285-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="3a285-110">Clean up deployment</span></span>

<span data-ttu-id="3a285-111">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="3a285-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3a285-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="3a285-112">Script explanation</span></span>

<span data-ttu-id="3a285-113">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="3a285-113">This script uses hello following commands.</span></span> <span data-ttu-id="3a285-114">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="3a285-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3a285-115">Comando</span><span class="sxs-lookup"><span data-stu-id="3a285-115">Command</span></span> | <span data-ttu-id="3a285-116">Notas</span><span class="sxs-lookup"><span data-stu-id="3a285-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a285-117">az group create</span><span class="sxs-lookup"><span data-stu-id="3a285-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="3a285-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="3a285-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3a285-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="3a285-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="3a285-120">Crea un servidor lógico que hospeda Hola base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3a285-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="3a285-121">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="3a285-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="3a285-122">Crea un tooall de acceso tooallow de regla de firewall bases de datos SQL en servidor de Hola de intervalo de direcciones IP de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="3a285-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="3a285-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="3a285-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="3a285-124">Crea Hola base de datos SQL en el servidor lógico Hola.</span><span class="sxs-lookup"><span data-stu-id="3a285-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="3a285-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="3a285-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="3a285-126">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="3a285-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a285-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3a285-127">Next steps</span></span>

<span data-ttu-id="3a285-128">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3a285-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3a285-129">Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de SQL en hello [documentación de la base de datos de SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3a285-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

