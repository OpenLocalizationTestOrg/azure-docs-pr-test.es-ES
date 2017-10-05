---
title: "PowerShell: Creación y administración de un grupo elástico de Azure SQL | Microsoft Docs"
description: "Aprenda a usar PowerShell para administrar un grupo elástico."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="c4e10-103">Creación y administración de un grupo elástico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4e10-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="c4e10-104">En este tema se muestra cómo crear y administrar [grupos elásticos](sql-database-elastic-pool.md) escalables con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4e10-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="c4e10-105">También puede crear y administrar un grupo elástico de Azure mediante [Azure Portal](https://portal.azure.com/), la API de REST o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c4e10-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="c4e10-106">También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="c4e10-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="c4e10-107">Creación de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-107">Create an elastic pool</span></span>
<span data-ttu-id="c4e10-108">El cmdlet [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) crea un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="c4e10-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="c4e10-109">Los valores de eDTU por grupo, DTU mín. y máx. están limitados por el valor de nivel de servicio (Básico, Estándar, Premium y Premium RS).</span><span class="sxs-lookup"><span data-stu-id="c4e10-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="c4e10-110">Consulte la sección [Límites de almacenamiento y de eDTU para grupos elásticos y bases de datos agrupadas](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="c4e10-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="c4e10-111">Creación de una base de datos agrupada en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="c4e10-112">Use el cmdlet [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) y establezca el parámetro **ElasticPoolName** en el grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="c4e10-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="c4e10-113">Para mover una base de datos existente a un grupo elástico, consulte [Movimiento de una base de datos a un grupo elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="c4e10-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="c4e10-114">Completar script</span><span class="sxs-lookup"><span data-stu-id="c4e10-114">Complete script</span></span>
<span data-ttu-id="c4e10-115">Este script crea un grupo de recursos de Azure y un servidor.</span><span class="sxs-lookup"><span data-stu-id="c4e10-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="c4e10-116">Cuando se le solicite, proporcione un nombre de usuario y una contraseña de administrador para el nuevo servidor (no las credenciales de Azure).</span><span class="sxs-lookup"><span data-stu-id="c4e10-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="c4e10-117">Creación de un grupo elástico y adición de varias bases de datos agrupadas</span><span class="sxs-lookup"><span data-stu-id="c4e10-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="c4e10-118">La creación de varias bases de datos en un grupo elástico puede tardar tiempo cuando se realiza mediante el portal o los cmdlets de PowerShell que crean una base de datos única cada vez.</span><span class="sxs-lookup"><span data-stu-id="c4e10-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="c4e10-119">Para automatizar la creación de un grupo elástico, consulte [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="c4e10-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="c4e10-120">Movimiento de una base de datos a un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="c4e10-121">Puede mover una base de datos dentro o fuera de un grupo elástico con el cmdlet [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="c4e10-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="c4e10-122">Cambio de la configuración de rendimiento de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="c4e10-123">Cuando el rendimiento se ve afectado, puede cambiar la configuración del grupo para adaptarse al crecimiento.</span><span class="sxs-lookup"><span data-stu-id="c4e10-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="c4e10-124">Utilice el cmdlet [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="c4e10-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="c4e10-125">Establezca el parámetro -Dtu en las eDTU por grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="c4e10-126">Consulte los posibles valores en el artículo sobre [límites de almacenamiento y de eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="c4e10-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="c4e10-127">Cambio del límite de almacenamiento de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="c4e10-128">Use el cmdlet [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) para establecer el parámetro _-StorageMB_.</span><span class="sxs-lookup"><span data-stu-id="c4e10-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="c4e10-129">Especifique el límite de almacenamiento en MB (por ejemplo, 2097152 establece el límite de almacenamiento en 2 TB).</span><span class="sxs-lookup"><span data-stu-id="c4e10-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="c4e10-130">Consulte los posibles valores en el artículo sobre [límites de almacenamiento y de eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="c4e10-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4e10-131">El almacenamiento de datos máximo predeterminado por grupo en el caso de los grupos Premium con 1500 eDTU, o más, es 750 GB.</span><span class="sxs-lookup"><span data-stu-id="c4e10-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="c4e10-132">Para obtener el mayor valor de _tamaño de almacenamiento de datos máximo por grupo_, se debe establecer explícitamente el límite de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c4e10-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="c4e10-133">Los grupos Premium con más de 750 GB de almacenamiento se encuentran actualmente en versión preliminar pública en las siguientes regiones: Este de EE. UU. 2, oeste de EE. UU., Virginia Gob. EE. UU., Europa Occidental, Centro de Alemania, Asia Suroriental, Japón Oriental, Este de Australia, centro de Canadá y Este de Canadá.</span><span class="sxs-lookup"><span data-stu-id="c4e10-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="c4e10-134">Obtención del estado de las operaciones de los grupos</span><span class="sxs-lookup"><span data-stu-id="c4e10-134">Get the status of pool operations</span></span>
<span data-ttu-id="c4e10-135">La creación de un grupo elástico puede llevar tiempo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="c4e10-136">Puede realizar un seguimiento del estado de las operaciones del grupo, como la creación y las actualizaciones, mediante el cmdlet [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity).</span><span class="sxs-lookup"><span data-stu-id="c4e10-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="c4e10-137">Obtención del estado del movimiento de una base de datos dentro y fuera de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="c4e10-138">El proceso de mover bases de datos puede llevar tiempo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-138">Moving a database can take time.</span></span> <span data-ttu-id="c4e10-139">Realice un seguimiento del estado del movimiento mediante el cmdlet [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity).</span><span class="sxs-lookup"><span data-stu-id="c4e10-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="c4e10-140">Obtención de datos de uso de recursos para un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="c4e10-141">Métricas que se pueden recuperar como porcentaje del límite del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="c4e10-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="c4e10-142">Nombre de métrica</span><span class="sxs-lookup"><span data-stu-id="c4e10-142">Metric name</span></span> | <span data-ttu-id="c4e10-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="c4e10-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c4e10-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="c4e10-144">cpu\_percent</span></span> |<span data-ttu-id="c4e10-145">Uso de proceso medio en porcentaje del límite del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="c4e10-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="c4e10-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="c4e10-147">Uso de E/S medio en porcentaje basado en el límite del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="c4e10-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="c4e10-148">log\_write\_percent</span></span> |<span data-ttu-id="c4e10-149">Uso de recursos de escritura medio en porcentaje del límite del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="c4e10-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="c4e10-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="c4e10-151">Uso de eDTU medio en porcentaje del límite de eDTU del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="c4e10-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="c4e10-152">storage\_percent</span></span> |<span data-ttu-id="c4e10-153">Uso de almacenamiento medio en porcentaje del límite de almacenamiento del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="c4e10-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="c4e10-154">workers\_percent</span></span> |<span data-ttu-id="c4e10-155">Cantidad máxima de trabajos simultáneos (solicitudes) en porcentaje basado en el límite del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="c4e10-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="c4e10-156">sessions\_percent</span></span> |<span data-ttu-id="c4e10-157">Cantidad máxima de sesiones simultáneas en porcentaje basado en el límite del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="c4e10-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="c4e10-158">eDTU_limit</span></span> |<span data-ttu-id="c4e10-159">Configuración de cantidad máxima de DTU de grupos elásticos actual para este grupo elástico durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="c4e10-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="c4e10-160">storage\_limit</span></span> |<span data-ttu-id="c4e10-161">Configuración de límite máximo de almacenamiento de grupos elásticos actual para este grupo elástico en megabytes durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="c4e10-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="c4e10-162">eDTU\_used</span></span> |<span data-ttu-id="c4e10-163">Cantidad media de eDTU que usa el grupo en este intervalo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="c4e10-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="c4e10-164">storage\_used</span></span> |<span data-ttu-id="c4e10-165">Cantidad media de almacenamiento en bytes que usa el grupo en este intervalo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="c4e10-166">**Métricas de períodos de retención y granularidad:**</span><span class="sxs-lookup"><span data-stu-id="c4e10-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="c4e10-167">Los datos se devuelven con una granularidad de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="c4e10-168">La retención de datos es de 35 días.</span><span class="sxs-lookup"><span data-stu-id="c4e10-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="c4e10-169">Este cmdlet y la API limitan el número de filas que se pueden recuperar en una llamada a 1000 filas (aproximadamente 3 días de datos con una granularidad de 5 minutos).</span><span class="sxs-lookup"><span data-stu-id="c4e10-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="c4e10-170">Sin embargo, este comando se puede llamar varias veces con distintos intervalos de tiempo de inicio y fin para recuperar más datos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="c4e10-171">Para recuperar las métricas, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c4e10-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="c4e10-172">Obtención de datos de uso de recursos de una base de datos en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="c4e10-173">Estas API son las mismas que las API que se utilizan para supervisar el uso de recursos de una base de datos única, salvo por la diferencia semántica siguiente: las métricas recuperadas se expresan como un porcentaje del eDTU máximo por base de datos (o límite equivalente para la métrica subyacente como CPU o E/S) establecido para ese grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="c4e10-174">Por ejemplo, el 50 % de uso de cualquiera de estas métricas indica que el consumo de recursos específicos es del 50 % del límite de capacidad por cada base de datos de dicho recurso del grupo principal.</span><span class="sxs-lookup"><span data-stu-id="c4e10-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="c4e10-175">Para recuperar las métricas, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c4e10-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="c4e10-176">Adición de una alerta a un recurso de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="c4e10-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="c4e10-177">Puede agregar reglas de alerta a un grupo elástico para enviar notificaciones por correo electrónico o cadenas de alertas a [puntos de conexión de URL](https://msdn.microsoft.com/library/mt718036.aspx) cuando un grupo elástico alcanza el umbral de utilización establecido.</span><span class="sxs-lookup"><span data-stu-id="c4e10-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="c4e10-178">Use el cmdlet Add-AzureRmMetricAlertRule.</span><span class="sxs-lookup"><span data-stu-id="c4e10-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4e10-179">La supervisión del uso de recursos de grupos elásticos tiene un retraso de, al menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="c4e10-180">En estos momentos, no se pueden establecer alertas de menos de 10 minutos para grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="c4e10-181">Las alertas establezcan para grupos elásticos con un período (parámetro denominado "-WindowSize" en la API de PowerShell) de menos de 10 minutos. no se puede desencadenar.</span><span class="sxs-lookup"><span data-stu-id="c4e10-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="c4e10-182">Asegúrese de que las alertas que defina para grupos elásticos utilicen un período (WindowSize) de 10 minutos o más.</span><span class="sxs-lookup"><span data-stu-id="c4e10-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="c4e10-183">En este ejemplo se agrega una alerta para recibir una notificación cuando el consumo de eDTU de un grupo elástico supere un umbral determinado.</span><span class="sxs-lookup"><span data-stu-id="c4e10-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="c4e10-184">Para más información, consulte cómo [crear alertas de SQL Database en Azure Portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4e10-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="c4e10-185">Adición de alertas a todas las bases de datos de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="c4e10-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="c4e10-186">Puede agregar reglas de alerta a todas las bases de datos de un grupo elástico para enviar notificaciones por correo electrónico o cadenas de alerta a [puntos de conexión de URL](https://msdn.microsoft.com/library/mt718036.aspx) cuando un recurso alcanza el umbral de utilización establecido por la alerta.</span><span class="sxs-lookup"><span data-stu-id="c4e10-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4e10-187">La supervisión del uso de recursos de grupos elásticos tiene un retraso de, al menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="c4e10-188">En estos momentos, no se pueden establecer alertas de menos de 10 minutos para grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="c4e10-189">Las alertas establezcan para grupos elásticos con un período (parámetro denominado "-WindowSize" en la API de PowerShell) de menos de 10 minutos. no se puede desencadenar.</span><span class="sxs-lookup"><span data-stu-id="c4e10-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="c4e10-190">Asegúrese de que las alertas que defina para grupos elásticos utilicen un período (WindowSize) de 10 minutos o más.</span><span class="sxs-lookup"><span data-stu-id="c4e10-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="c4e10-191">En este ejemplo se agrega una alerta a cada una de las bases de datos de un grupo elástico para recibir una notificación cuando el consumo de DTU de esas bases de datos supere un umbral determinado.</span><span class="sxs-lookup"><span data-stu-id="c4e10-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="c4e10-192">Recopilación y supervisión de los datos de uso de recursos entre varios grupos de una suscripción</span><span class="sxs-lookup"><span data-stu-id="c4e10-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="c4e10-193">Si hay muchas bases de datos en una suscripción, es complicado supervisar cada grupo elástico por separado.</span><span class="sxs-lookup"><span data-stu-id="c4e10-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="c4e10-194">En su lugar, se pueden combinar las consultas de T-SQL y los cmdlets de PowerShell de Base de datos SQL para recopilar datos de uso de recursos de varios grupos y sus bases de datos para la supervisión y el análisis del uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="c4e10-195">Puede encontrar una [implementación de ejemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) de un conjunto similar de scripts de PowerShell en el repositorio de ejemplos de SQL Server de GitHub junto con documentación sobre lo que hace y cómo se utiliza.</span><span class="sxs-lookup"><span data-stu-id="c4e10-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="c4e10-196">Para utilizar esta implementación de ejemplo siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="c4e10-197">Descargue los [scripts y la documentación](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="c4e10-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="c4e10-198">Modifique los scripts para su entorno.</span><span class="sxs-lookup"><span data-stu-id="c4e10-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="c4e10-199">Especifique uno o más servidores en los que se alojan los grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="c4e10-200">Especifique una base de datos de telemetría donde se puedan almacenar las métricas recopiladas.</span><span class="sxs-lookup"><span data-stu-id="c4e10-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="c4e10-201">Personalice el script para especificar el tiempo de ejecución de los scripts.</span><span class="sxs-lookup"><span data-stu-id="c4e10-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="c4e10-202">En un nivel alto, los scripts realizan lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c4e10-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="c4e10-203">Enumera todos los servidores de una determinada suscripción de Azure (o una lista de servidores especificada).</span><span class="sxs-lookup"><span data-stu-id="c4e10-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="c4e10-204">Ejecuta un trabajo en segundo plano para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="c4e10-204">Runs a background job for each server.</span></span> <span data-ttu-id="c4e10-205">El trabajo se ejecuta en un bucle a intervalos regulares y recopila los datos de telemetría de todos los grupos en el servidor.</span><span class="sxs-lookup"><span data-stu-id="c4e10-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="c4e10-206">A continuación, carga los datos recopilados en la base de datos de telemetría especificada.</span><span class="sxs-lookup"><span data-stu-id="c4e10-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="c4e10-207">Enumera una lista de bases de datos en cada grupo para recopilar los datos de uso de recursos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="c4e10-208">A continuación, carga los datos recopilados en la base de datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="c4e10-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="c4e10-209">Para supervisar el estado de los grupos elásticos y de las bases de datos en tales grupos, se pueden analizar las métricas recopiladas en la base de datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="c4e10-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="c4e10-210">El script también instala una función de valores de tabla (TVF) predefinida en la base de datos de telemetría para ayudar a agregar las métricas para un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="c4e10-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="c4e10-211">Por ejemplo, los resultados de la función TVF pueden utilizarse para mostrar "los N grupos elásticos que presentan el máximo uso de eDTU en un período de tiempo determinado".</span><span class="sxs-lookup"><span data-stu-id="c4e10-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="c4e10-212">Opcionalmente, puede utilizar herramientas de análisis como Excel o Power BI para consultar y analizar los datos recopilados.</span><span class="sxs-lookup"><span data-stu-id="c4e10-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="c4e10-213">Ejemplo: recuperación de métricas de consumo de recursos de un grupo elástico y de sus bases de datos</span><span class="sxs-lookup"><span data-stu-id="c4e10-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="c4e10-214">En este ejemplo se recuperan las métricas de consumo de un grupo elástico determinado y de todas sus bases de datos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="c4e10-215">Se da formato a los datos recopilados y se escriben en un archivo .csv.</span><span class="sxs-lookup"><span data-stu-id="c4e10-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="c4e10-216">El archivo puede consultarse con Excel.</span><span class="sxs-lookup"><span data-stu-id="c4e10-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="c4e10-217">Latencia de las operaciones de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="c4e10-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="c4e10-218">El cambio del número mínimo de eDTU por base de datos o del máximo de eDTU por base de datos suele completarse en cinco minutos o menos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="c4e10-219">El cambio de eDTU por grupo depende de la cantidad total de espacio que usen todas las bases de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="c4e10-220">Los cambios tienen un duración media de 90 minutos o menos por cada 100 GB.</span><span class="sxs-lookup"><span data-stu-id="c4e10-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="c4e10-221">Por ejemplo, si el espacio total que usan todas las bases de datos del grupo es de 200 GB, la latencia esperada para cambiar las eDTU de grupo por grupo es de 3 horas o menos.</span><span class="sxs-lookup"><span data-stu-id="c4e10-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c4e10-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4e10-222">Next steps</span></span>
* <span data-ttu-id="c4e10-223">[Creación de trabajos elásticos](sql-database-elastic-jobs-overview.md) : los trabajos elásticos le permiten ejecutar scripts de T-SQL en cualquier cantidad de bases de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="c4e10-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="c4e10-224">Consulte [Escalado horizontal con Azure SQL Database](sql-database-elastic-scale-introduction.md): use herramientas elásticas para realizar un escalado horizontal, mover los datos, realizar consultas o crear transacciones.</span><span class="sxs-lookup"><span data-stu-id="c4e10-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
