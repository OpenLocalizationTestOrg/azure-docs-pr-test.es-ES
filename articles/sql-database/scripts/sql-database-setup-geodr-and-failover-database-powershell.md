---
title: "aaaPowerShell ejemplo activo geográfica-replicación-solo la base de datos SQL Azure | Documentos de Microsoft"
description: "Azure tooset de script de ejemplo de PowerShell la replicación geográfica activa para una sola base de datos de SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 9ad424d313a5aa96e31b50a1a39c71fd346a7ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="0ea1a-103">Usar PowerShell tooconfigure replicación geográfica activa para una sola base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0ea1a-103">Use PowerShell tooconfigure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="0ea1a-104">En este ejemplo de secuencia de comandos de PowerShell configura la replicación geográfica activa para una sola base de datos de SQL Azure y se conmuta por error tooa de réplica de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="0ea1a-105">Scripts de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0ea1a-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0ea1a-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="0ea1a-106">Clean up deployment</span></span>

<span data-ttu-id="0ea1a-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0ea1a-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0ea1a-108">Script explanation</span></span>

<span data-ttu-id="0ea1a-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-109">This script uses hello following commands.</span></span> <span data-ttu-id="0ea1a-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0ea1a-111">Comando</span><span class="sxs-lookup"><span data-stu-id="0ea1a-111">Command</span></span> | <span data-ttu-id="0ea1a-112">Notas</span><span class="sxs-lookup"><span data-stu-id="0ea1a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0ea1a-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ea1a-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0ea1a-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0ea1a-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="0ea1a-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0ea1a-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="0ea1a-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="0ea1a-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="0ea1a-118">Crea un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="0ea1a-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0ea1a-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="0ea1a-120">Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="0ea1a-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0ea1a-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="0ea1a-122">Crea una base de datos secundaria para una base de datos existente e inicia la replicación de datos.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="0ea1a-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0ea1a-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="0ea1a-124">Obtiene una o más bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="0ea1a-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0ea1a-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="0ea1a-126">Se activa una conmutación por error de base de datos secundaria toobe tooinitiate principal.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="0ea1a-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="0ea1a-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="0ea1a-128">Obtiene los vínculos de replicación geográfica de hello entre una base de datos de SQL Azure y un grupo de recursos o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="0ea1a-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0ea1a-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="0ea1a-130">Finaliza la replicación de datos entre una base de datos SQL y la base de datos secundaria Hola especificado.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="0ea1a-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ea1a-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0ea1a-132">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="0ea1a-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="0ea1a-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ea1a-133">Next steps</span></span>

<span data-ttu-id="0ea1a-134">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0ea1a-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0ea1a-135">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0ea1a-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
