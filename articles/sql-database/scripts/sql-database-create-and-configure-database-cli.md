---
title: Ejemplo de la CLI para crear una instancia de Azure SQL Database | Microsoft Docs
description: Ejemplo de script de la CLI de Azure para crear una base de datos SQL
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
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="6c300-103">Uso de la CLI para crear una instancia única de Azure SQL Database y configurar una regla de firewall</span><span class="sxs-lookup"><span data-stu-id="6c300-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="6c300-104">Este script de ejemplo de la CLI de Azure crea una instancia de Azure SQL Database y configura una regla de firewall en el nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="6c300-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="6c300-105">Después de ejecutar el script correctamente, la base de datos SQL es accesible desde todos los servicios de Azure y la dirección IP configurada.</span><span class="sxs-lookup"><span data-stu-id="6c300-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6c300-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="6c300-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6c300-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="6c300-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="6c300-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c300-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6c300-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6c300-109">Sample script</span></span>

<span data-ttu-id="6c300-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Creación de una base de datos SQL")]</span><span class="sxs-lookup"><span data-stu-id="6c300-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6c300-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="6c300-111">Clean up deployment</span></span>

<span data-ttu-id="6c300-112">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="6c300-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6c300-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6c300-113">Script explanation</span></span>

<span data-ttu-id="6c300-114">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="6c300-114">This script uses the following commands.</span></span> <span data-ttu-id="6c300-115">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="6c300-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6c300-116">Comando</span><span class="sxs-lookup"><span data-stu-id="6c300-116">Command</span></span> | <span data-ttu-id="6c300-117">Notas</span><span class="sxs-lookup"><span data-stu-id="6c300-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c300-118">az group create</span><span class="sxs-lookup"><span data-stu-id="6c300-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6c300-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6c300-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c300-120">az sql server create</span><span class="sxs-lookup"><span data-stu-id="6c300-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="6c300-121">Crea un servidor lógico que hospeda la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="6c300-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="6c300-122">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="6c300-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="6c300-123">Crea una regla de firewall para permitir el acceso a todas las bases de datos SQL en el servidor desde el intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="6c300-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="6c300-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="6c300-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="6c300-125">Crea una base de datos SQL en el servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="6c300-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="6c300-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="6c300-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="6c300-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="6c300-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c300-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c300-128">Next steps</span></span>

<span data-ttu-id="6c300-129">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c300-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c300-130">Encontrará más ejemplos de scripts de la CLI de SQL Database en la [documentación de Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6c300-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

