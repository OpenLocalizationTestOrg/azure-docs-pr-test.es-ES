---
title: base de datos de SQL de Azure de ejemplo-monitor-escala-individual de aaaCLI | Documentos de Microsoft
description: Azure toomonitor de secuencia de comandos de ejemplo CLI y la escala una sola base de datos de SQL Azure
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="7ab8b-103">Usar toomonitor CLI y escalar una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="7ab8b-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="7ab8b-104">En este ejemplo de secuencia de comandos de CLI de Azure se escala un solo nivel de rendimiento de tooa de base de datos SQL de Azure después de consultar información sobre el tamaño de base de datos de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7ab8b-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7ab8b-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7ab8b-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7ab8b-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7ab8b-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7ab8b-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7ab8b-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="7ab8b-109">Clean up deployment</span></span>

<span data-ttu-id="7ab8b-110">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7ab8b-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="7ab8b-111">Script explanation</span></span>

<span data-ttu-id="7ab8b-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-112">This script uses hello following commands.</span></span> <span data-ttu-id="7ab8b-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7ab8b-114">Comando</span><span class="sxs-lookup"><span data-stu-id="7ab8b-114">Command</span></span> | <span data-ttu-id="7ab8b-115">Notas</span><span class="sxs-lookup"><span data-stu-id="7ab8b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7ab8b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="7ab8b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7ab8b-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7ab8b-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="7ab8b-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="7ab8b-119">Crea un servidor lógico que hospeda una base de datos.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="7ab8b-120">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="7ab8b-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="7ab8b-121">Muestra información de uso de tamaño de Hola para una base de datos.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="7ab8b-122">az sql db update</span><span class="sxs-lookup"><span data-stu-id="7ab8b-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="7ab8b-123">Actualiza las propiedades de la base de datos (por ejemplo, el nivel de rendimiento o de servicio de hello) o mueve una base de datos en, fuera de o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="7ab8b-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="7ab8b-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7ab8b-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="7ab8b-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="7ab8b-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7ab8b-126">Next steps</span></span>

<span data-ttu-id="7ab8b-127">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ab8b-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7ab8b-128">Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de SQL en hello [documentación de la base de datos de SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7ab8b-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
