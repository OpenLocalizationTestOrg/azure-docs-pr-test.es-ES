---
title: "PowerShell: Creación y administración de un grupo elástico de Azure SQL | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse PowerShell toomanage un grupo elástico."
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
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="017d7-103">Creación y administración de un grupo elástico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="017d7-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="017d7-104">Este tema muestra cómo toocreate y administrar escalable [grupos elásticos](sql-database-elastic-pool.md) con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="017d7-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="017d7-105">También puede crear y administrar un grupo elástico Azure con hello [portal de Azure](https://portal.azure.com/), API de REST, o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="017d7-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="017d7-106">También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="017d7-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="017d7-107">Creación de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-107">Create an elastic pool</span></span>
<span data-ttu-id="017d7-108">Hola [AzureRmSqlElasticPool New](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet crea un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="017d7-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="017d7-109">valores de Hello de eDTU por grupo, min y max Dtu están restringidos por el valor de nivel de servicio de hello (Basic, Standard, Premium o RS Premium).</span><span class="sxs-lookup"><span data-stu-id="017d7-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="017d7-110">Consulte la sección [Límites de almacenamiento y de eDTU para grupos elásticos y bases de datos agrupadas](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="017d7-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="017d7-111">Creación de una base de datos agrupada en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="017d7-112">Hola de uso [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet conjunto hello y **ElasticPoolName** bloque de destino de parámetro toohello.</span><span class="sxs-lookup"><span data-stu-id="017d7-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="017d7-113">Consulte una base de datos existente en un grupo elástico, toomove [mover una base de datos en un grupo elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="017d7-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="017d7-114">Completar script</span><span class="sxs-lookup"><span data-stu-id="017d7-114">Complete script</span></span>
<span data-ttu-id="017d7-115">Este script crea un grupo de recursos de Azure y un servidor.</span><span class="sxs-lookup"><span data-stu-id="017d7-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="017d7-116">Cuando se le solicite, proporcione un nombre de usuario de administrador y la contraseña de nuevo servidor de hello (no sus credenciales de Azure).</span><span class="sxs-lookup"><span data-stu-id="017d7-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="017d7-117">Creación de un grupo elástico y adición de varias bases de datos agrupadas</span><span class="sxs-lookup"><span data-stu-id="017d7-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="017d7-118">Creación de varias bases de datos en un grupo elástico puede tardar tiempo cuando se realiza mediante el portal de Hola o los cmdlets de PowerShell que crean una sola base de datos a la vez.</span><span class="sxs-lookup"><span data-stu-id="017d7-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="017d7-119">creación de tooautomate en un grupo elástico, consulte [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="017d7-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="017d7-120">Movimiento de una base de datos a un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="017d7-121">Puede mover una base de datos dentro o fuera de un grupo elástico con hello [AzureRmSqlDatabase conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="017d7-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="017d7-122">Cambio de la configuración de rendimiento de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="017d7-123">Cuando el rendimiento se ve afectado, puede cambiar configuración de Hola de crecimiento de hello grupo tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="017d7-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="017d7-124">Hola de uso [AzureRmSqlElasticPool conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="017d7-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="017d7-125">Establecer hello - Dtu parámetro toohello Edtu por grupo.</span><span class="sxs-lookup"><span data-stu-id="017d7-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="017d7-126">Consulte los posibles valores en el artículo sobre [límites de almacenamiento y de eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="017d7-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="017d7-127">Cambiar el límite de almacenamiento de Hola para un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="017d7-128">Hola de uso [conjunto AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _StorageMB -_ parámetro.</span><span class="sxs-lookup"><span data-stu-id="017d7-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="017d7-129">Proporcione el límite de almacenamiento de hello en MB (por ejemplo, 2097152 conjuntos Hola almacenamiento límite too2 TB).</span><span class="sxs-lookup"><span data-stu-id="017d7-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="017d7-130">Consulte los posibles valores en el artículo sobre [límites de almacenamiento y de eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="017d7-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="017d7-131">almacenamiento de datos max Hola predeterminado por grupo de grupos de Premium con Edtu de 1500 o más están 750 GB.</span><span class="sxs-lookup"><span data-stu-id="017d7-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="017d7-132">Hola tooobtain superior _máximo tamaño de almacenamiento de datos por grupo de_, se debe establecer explícitamente el límite de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="017d7-133">Grupos de Premium con más de 750 GB de almacenamiento está actualmente en versión preliminar pública Hola siguientes regiones: UU 2, oeste de Estados Unidos, nos Gov Virginia, Europa occidental, Central de Alemania, sudeste de Asia, este de Japón, Australia Oriental, Canadá Central y este de Canadá.</span><span class="sxs-lookup"><span data-stu-id="017d7-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="017d7-134">Obtener estado de Hola de las operaciones de grupo</span><span class="sxs-lookup"><span data-stu-id="017d7-134">Get hello status of pool operations</span></span>
<span data-ttu-id="017d7-135">La creación de un grupo elástico puede llevar tiempo.</span><span class="sxs-lookup"><span data-stu-id="017d7-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="017d7-136">estado de hello tootrack de las operaciones del fondo incluidos creación y las actualizaciones, utilice hello [AzureRmSqlElasticPoolActivity Get](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="017d7-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="017d7-137">Obtener estado de Hola de mover una base de datos dentro y fuera de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="017d7-138">El proceso de mover bases de datos puede llevar tiempo.</span><span class="sxs-lookup"><span data-stu-id="017d7-138">Moving a database can take time.</span></span> <span data-ttu-id="017d7-139">Realizar un seguimiento de un estado de movimiento mediante hello [AzureRmSqlDatabaseActivity Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="017d7-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="017d7-140">Obtención de datos de uso de recursos para un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="017d7-141">Métricas que se pueden recuperar como un porcentaje del límite de grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="017d7-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="017d7-142">Nombre de métrica</span><span class="sxs-lookup"><span data-stu-id="017d7-142">Metric name</span></span> | <span data-ttu-id="017d7-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="017d7-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="017d7-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="017d7-144">cpu\_percent</span></span> |<span data-ttu-id="017d7-145">Uso de proceso promedio expresado en porcentaje del límite de Hola de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="017d7-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="017d7-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="017d7-147">Uso promedio de E/S en porcentaje según Hola límite de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="017d7-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="017d7-148">log\_write\_percent</span></span> |<span data-ttu-id="017d7-149">Utilización de recursos de escritura promedio expresado en porcentaje del límite de Hola de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="017d7-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="017d7-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="017d7-151">Uso de eDTU promedio en porcentaje del límite de eDTU de grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="017d7-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="017d7-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="017d7-152">storage\_percent</span></span> |<span data-ttu-id="017d7-153">Promedio de utilización del almacenamiento de información como un porcentaje del límite de almacenamiento de Hola de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="017d7-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="017d7-154">workers\_percent</span></span> |<span data-ttu-id="017d7-155">Máximos simultáneos trabajadores (solicitudes) de porcentaje se basa en el límite de Hola de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="017d7-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="017d7-156">sessions\_percent</span></span> |<span data-ttu-id="017d7-157">Número máximo de sesiones simultáneo de porcentaje se basa en el límite de Hola de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="017d7-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="017d7-158">eDTU_limit</span></span> |<span data-ttu-id="017d7-159">Configuración de cantidad máxima de DTU de grupos elásticos actual para este grupo elástico durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="017d7-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="017d7-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="017d7-160">storage\_limit</span></span> |<span data-ttu-id="017d7-161">Configuración de límite máximo de almacenamiento de grupos elásticos actual para este grupo elástico en megabytes durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="017d7-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="017d7-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="017d7-162">eDTU\_used</span></span> |<span data-ttu-id="017d7-163">Edtu promedio utilizada por el grupo de hello en este intervalo.</span><span class="sxs-lookup"><span data-stu-id="017d7-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="017d7-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="017d7-164">storage\_used</span></span> |<span data-ttu-id="017d7-165">Almacenamiento medio utilizado por el grupo de hello en este intervalo de bytes</span><span class="sxs-lookup"><span data-stu-id="017d7-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="017d7-166">**Métricas de períodos de retención y granularidad:**</span><span class="sxs-lookup"><span data-stu-id="017d7-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="017d7-167">Los datos se devuelven con una granularidad de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="017d7-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="017d7-168">La retención de datos es de 35 días.</span><span class="sxs-lookup"><span data-stu-id="017d7-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="017d7-169">Este cmdlet y API limita el número de Hola de filas que se pueden recuperar en una llamada too1000 filas (aproximadamente 3 días de datos con granularidad de 5 minutos).</span><span class="sxs-lookup"><span data-stu-id="017d7-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="017d7-170">Pero este comando se puede llamar varias veces con tooretrieve de intervalos de tiempo de inicio y fin diferentes más datos</span><span class="sxs-lookup"><span data-stu-id="017d7-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="017d7-171">métricas de Hola tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="017d7-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="017d7-172">Obtención de datos de uso de recursos de una base de datos en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="017d7-173">Estas API son Hola igual Hola API que se usan para supervisar la utilización de recursos de Hola de una base de datos, excepto Hola después diferencia semántica: métricas recuperadas se expresan como un porcentaje de hello por Edtu de base de datos max (o cap equivalente para hello subyacente métrica como CPU o E/S) establecido para ese grupo.</span><span class="sxs-lookup"><span data-stu-id="017d7-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="017d7-174">Por ejemplo, 50% de utilización de cualquiera de estas métricas indica que el consumo de recursos específicos de hello es en el 50% de hello por límite de base de datos para ese recurso en el grupo primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="017d7-175">métricas de Hola tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="017d7-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="017d7-176">Agregar un recurso de grupo elástico tooan alerta</span><span class="sxs-lookup"><span data-stu-id="017d7-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="017d7-177">Puede agregar reglas de alerta tooan grupo elástico toosend notificaciones por correo electrónico o las cadenas de alerta demasiado[puntos de conexión URL](https://msdn.microsoft.com/library/mt718036.aspx) al grupo elástico Hola alcanza un umbral de uso que configuró.</span><span class="sxs-lookup"><span data-stu-id="017d7-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="017d7-178">Use el cmdlet de hello AzureRmMetricAlertRule agregar.</span><span class="sxs-lookup"><span data-stu-id="017d7-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="017d7-179">La supervisión del uso de recursos de grupos elásticos tiene un retraso de, al menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="017d7-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="017d7-180">En estos momentos, no se pueden establecer alertas de menos de 10 minutos para grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="017d7-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="017d7-181">Las alertas establezcan para grupos elásticos con un período (parámetro denominado "-WindowSize" en la API de PowerShell) de menos de 10 minutos. no se puede desencadenar.</span><span class="sxs-lookup"><span data-stu-id="017d7-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="017d7-182">Asegúrese de que las alertas que defina para grupos elásticos utilicen un período (WindowSize) de 10 minutos o más.</span><span class="sxs-lookup"><span data-stu-id="017d7-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="017d7-183">En este ejemplo se agrega una alerta para recibir una notificación cuando el consumo de eDTU de un grupo elástico supere un umbral determinado.</span><span class="sxs-lookup"><span data-stu-id="017d7-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="017d7-184">Para más información, consulte cómo [crear alertas de SQL Database en Azure Portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="017d7-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="017d7-185">Agregar bases de datos de alertas tooall en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="017d7-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="017d7-186">Puede agregar reglas de alerta tooall base de datos en un grupo elástico toosend notificaciones por correo electrónico o las cadenas de alerta demasiado[puntos de conexión URL](https://msdn.microsoft.com/library/mt718036.aspx) cuando un recurso alcanza un umbral de utilización de configurar la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="017d7-187">La supervisión del uso de recursos de grupos elásticos tiene un retraso de, al menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="017d7-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="017d7-188">En estos momentos, no se pueden establecer alertas de menos de 10 minutos para grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="017d7-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="017d7-189">Las alertas establezcan para grupos elásticos con un período (parámetro denominado "-WindowSize" en la API de PowerShell) de menos de 10 minutos. no se puede desencadenar.</span><span class="sxs-lookup"><span data-stu-id="017d7-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="017d7-190">Asegúrese de que las alertas que defina para grupos elásticos utilicen un período (WindowSize) de 10 minutos o más.</span><span class="sxs-lookup"><span data-stu-id="017d7-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="017d7-191">Este ejemplo agrega una alerta tooeach de bases de datos de hello en un grupo elástico para recibir una notificación cuando el consumo de DTU de esa base de datos está por encima de cierto umbral.</span><span class="sxs-lookup"><span data-stu-id="017d7-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="017d7-192">Recopilación y supervisión de los datos de uso de recursos entre varios grupos de una suscripción</span><span class="sxs-lookup"><span data-stu-id="017d7-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="017d7-193">Cuando se tienen muchas bases de datos en una suscripción, es toomonitor complicada cada flexible del grupo por separado.</span><span class="sxs-lookup"><span data-stu-id="017d7-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="017d7-194">En su lugar, los cmdlets de PowerShell de base de datos SQL y las consultas de T-SQL pueden ser toocollect combinados los datos de uso de recursos de varios grupos y sus bases de datos para la supervisión y análisis de uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="017d7-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="017d7-195">A [implementación del ejemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) de este tipo de un conjunto de powershell scripts pueden encontrarse en el repositorio de ejemplos de hello GitHub SQL Server junto con documentación en lo que hace y cómo toouse lo.</span><span class="sxs-lookup"><span data-stu-id="017d7-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="017d7-196">toouse esta implementación de ejemplo, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="017d7-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="017d7-197">Descargar hello [scripts y más documentación](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="017d7-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="017d7-198">Modifique los scripts de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="017d7-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="017d7-199">Especifique uno o más servidores en los que se alojan los grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="017d7-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="017d7-200">Especifique una base de datos de telemetría donde hello recopiladas métricas son toobe almacenado.</span><span class="sxs-lookup"><span data-stu-id="017d7-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="017d7-201">Personalizar Hola script toospecify Hola dure la ejecución de las secuencias de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="017d7-202">En un nivel alto, las secuencias de comandos de Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="017d7-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="017d7-203">Enumera todos los servidores de una determinada suscripción de Azure (o una lista de servidores especificada).</span><span class="sxs-lookup"><span data-stu-id="017d7-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="017d7-204">Ejecuta un trabajo en segundo plano para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="017d7-204">Runs a background job for each server.</span></span> <span data-ttu-id="017d7-205">trabajo de Hola se ejecuta en un bucle a intervalos regulares y recopila los datos de telemetría para todos los grupos de hello en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="017d7-206">A continuación, carga Hola recopilan datos en la base de datos de telemetría especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="017d7-207">Enumera la lista de bases de datos de cada datos de uso de recursos de base de datos de grupo toocollect Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="017d7-208">A continuación, carga Hola recopilan datos en la base de datos de telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="017d7-209">Hello recopilados las métricas de base de datos de telemetría de Hola pueden ser analizados toomonitor Hola Mantenimiento grupos elásticos y bases de datos de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="017d7-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="017d7-210">script de Hola también instala una función de valores de tabla (TVF) predefinida en métricas Hola agregado toohelp de base de datos de telemetría de Hola para un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="017d7-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="017d7-211">Por ejemplo, puede ser resultado de hello TVF usa tooshow "top N grupos elásticos con un uso máximo de eDTU hello en un período de tiempo determinado."</span><span class="sxs-lookup"><span data-stu-id="017d7-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="017d7-212">Si lo desea, usar herramientas analíticas, como Excel o Power BI tooquery y analizar los datos recopilado de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="017d7-213">Ejemplo: recuperación de métricas de consumo de recursos de un grupo elástico y de sus bases de datos</span><span class="sxs-lookup"><span data-stu-id="017d7-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="017d7-214">Este ejemplo recupera las métricas de consumo de Hola para un determinado grupo elástico y todas sus bases de datos.</span><span class="sxs-lookup"><span data-stu-id="017d7-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="017d7-215">Los datos recopilados es el formato y escritos el archivo con formato .csv de tooa.</span><span class="sxs-lookup"><span data-stu-id="017d7-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="017d7-216">se pueden examinar el archivo Hello con Excel.</span><span class="sxs-lookup"><span data-stu-id="017d7-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
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

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="017d7-217">Latencia de las operaciones de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="017d7-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="017d7-218">Cambiar normalmente Hola min Edtu por base de datos o el número máximo de Edtu por base de datos completa en 5 minutos o menos.</span><span class="sxs-lookup"><span data-stu-id="017d7-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="017d7-219">Cambiar hello Edtu por grupo de depende de la cantidad total de Hola de espacio utilizado por todas las bases de datos de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="017d7-220">Los cambios tienen un duración media de 90 minutos o menos por cada 100 GB.</span><span class="sxs-lookup"><span data-stu-id="017d7-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="017d7-221">Por ejemplo, si utiliza el espacio total de Hola por todas las bases de datos de grupo de hello es de 200 GB, Hola espera latencia para cambiar hello eDTU del grupo por grupo es de 3 horas o menos.</span><span class="sxs-lookup"><span data-stu-id="017d7-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="017d7-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="017d7-222">Next steps</span></span>
* <span data-ttu-id="017d7-223">[Crear trabajos elásticos](sql-database-elastic-jobs-overview.md) trabajos elásticos le permiten ejecutar scripts T-SQL en cualquier número de bases de datos de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="017d7-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="017d7-224">Vea [escalado horizontal con base de datos de SQL Azure](sql-database-elastic-scale-introduction.md): usar herramientas elásticas tooscale out, mover los datos, consultar o crear las transacciones.</span><span class="sxs-lookup"><span data-stu-id="017d7-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
