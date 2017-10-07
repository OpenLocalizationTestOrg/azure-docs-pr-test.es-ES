---
title: "base de datos SQL de Azure agrupadas de replicación geográfica de activos de ejemplo aaaPowerShell | Documentos de Microsoft"
description: "Azure tooset de script de ejemplo de PowerShell la replicación geográfica activa para una base de datos de Azure SQL agrupado"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="39575-103">Usar PowerShell tooconfigure replicación geográfica activa para una base de datos de Azure SQL agrupado</span><span class="sxs-lookup"><span data-stu-id="39575-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="39575-104">En este ejemplo de secuencia de comandos de PowerShell configura la replicación geográfica activa para una base de datos de SQL Azure en un grupo elástico y se conmuta por error toohello de réplica de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="39575-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="39575-105">Scripts de ejemplo</span><span class="sxs-lookup"><span data-stu-id="39575-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="39575-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="39575-106">Clean up deployment</span></span>

<span data-ttu-id="39575-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="39575-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="39575-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="39575-108">Script explanation</span></span>

<span data-ttu-id="39575-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="39575-109">This script uses hello following commands.</span></span> <span data-ttu-id="39575-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="39575-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="39575-111">Comando</span><span class="sxs-lookup"><span data-stu-id="39575-111">Command</span></span> | <span data-ttu-id="39575-112">Notas</span><span class="sxs-lookup"><span data-stu-id="39575-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39575-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="39575-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="39575-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="39575-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="39575-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="39575-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="39575-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="39575-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="39575-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="39575-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="39575-118">Crea un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="39575-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="39575-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="39575-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="39575-120">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="39575-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="39575-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="39575-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="39575-122">Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="39575-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="39575-123">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="39575-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="39575-124">Crea una base de datos secundaria para una base de datos existente e inicia la replicación de datos.</span><span class="sxs-lookup"><span data-stu-id="39575-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="39575-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="39575-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="39575-126">Obtiene una o más bases de datos.</span><span class="sxs-lookup"><span data-stu-id="39575-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="39575-127">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="39575-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="39575-128">Base de datos secundaria toobe principal se activa en conmutación por error de orden tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="39575-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="39575-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="39575-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="39575-130">Obtiene los vínculos de replicación geográfica de hello entre una base de datos de SQL Azure y un grupo de recursos o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39575-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="39575-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="39575-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="39575-132">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="39575-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="39575-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39575-133">Next steps</span></span>

<span data-ttu-id="39575-134">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="39575-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="39575-135">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="39575-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
