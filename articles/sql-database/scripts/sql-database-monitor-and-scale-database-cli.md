---
title: Ejemplo de la CLI para supervisar y escalar una instancia de Azure SQL Database | Microsoft Docs
description: Script de ejemplo de la CLI de Azure para supervisar y escalar una instancia de Azure SQL Database
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
ms.openlocfilehash: 01911b85268244a8fddb32aa726f8a870abbaf77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="f7598-103">Uso de la CLI para supervisar y escalar una instancia de SQL Database</span><span class="sxs-lookup"><span data-stu-id="f7598-103">Use CLI to monitor and scale a single SQL database</span></span>

<span data-ttu-id="f7598-104">Este ejemplo de script de la CLI de Azure escala una sola instancia de Azure SQL Database a un nivel de rendimiento distinto después de consultar la información del tamaño de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f7598-104">This Azure CLI script example scales a single Azure SQL database to a different performance level after querying the size information of the database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f7598-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f7598-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f7598-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="f7598-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f7598-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f7598-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f7598-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f7598-108">Sample script</span></span>

<span data-ttu-id="f7598-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Supervisión y escalado de una instancia única de SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="f7598-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f7598-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="f7598-110">Clean up deployment</span></span>

<span data-ttu-id="f7598-111">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="f7598-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f7598-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f7598-112">Script explanation</span></span>

<span data-ttu-id="f7598-113">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="f7598-113">This script uses the following commands.</span></span> <span data-ttu-id="f7598-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="f7598-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f7598-115">Comando</span><span class="sxs-lookup"><span data-stu-id="f7598-115">Command</span></span> | <span data-ttu-id="f7598-116">Notas</span><span class="sxs-lookup"><span data-stu-id="f7598-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f7598-117">az group create</span><span class="sxs-lookup"><span data-stu-id="f7598-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f7598-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f7598-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f7598-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="f7598-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="f7598-120">Crea un servidor lógico que hospeda una base de datos.</span><span class="sxs-lookup"><span data-stu-id="f7598-120">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="f7598-121">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="f7598-121">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="f7598-122">Muestra la información de uso del tamaño de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="f7598-122">Shows the size usage information for a database.</span></span> |
| [<span data-ttu-id="f7598-123">az sql db update</span><span class="sxs-lookup"><span data-stu-id="f7598-123">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="f7598-124">Actualiza las propiedades de la base de datos (por ejemplo, el nivel de rendimiento o el de servicio), o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="f7598-124">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="f7598-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="f7598-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f7598-126">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="f7598-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="f7598-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f7598-127">Next steps</span></span>

<span data-ttu-id="f7598-128">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f7598-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f7598-129">Encontrará más ejemplos de scripts de la CLI de SQL Database en la [documentación de Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f7598-129">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
