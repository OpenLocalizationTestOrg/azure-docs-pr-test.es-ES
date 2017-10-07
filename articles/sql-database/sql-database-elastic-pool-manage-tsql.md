---
title: "T-SQL: Administración de un grupo elástico de Azure SQL Database | Microsoft Docs"
description: "Usar T-SQL toomanage un grupo elástico de base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="7e2ad-103">Supervisión y administración de un grupo elástico con Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="7e2ad-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="7e2ad-104">Este tema muestra cómo toomanage escalable [grupos elásticos](sql-database-elastic-pool.md) con Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="7e2ad-105">También puede crear y administrar un hello Azure grupo elástico [portal de Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), API de REST de Hola o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7e2ad-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="7e2ad-106">También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="7e2ad-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="7e2ad-107">Hola de uso [Create Database (base de datos de SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) y [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) comandos toocreate y mover bases de datos dentro y fuera de grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="7e2ad-108">grupo elástico Hola debe existir para poder utilizar estos comandos.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="7e2ad-109">Estos comandos afectan solo a las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-109">These commands affect only databases.</span></span> <span data-ttu-id="7e2ad-110">Creación de grupos nuevos y Hola establecer propiedades de grupo (por ejemplo, min y max Edtu) no se puede cambiar con comandos de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="7e2ad-111">Creación de una base de datos agrupada en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="7e2ad-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="7e2ad-112">Usar el comando CREATE DATABASE de Hola con Hola opción SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="7e2ad-113">Todas las bases de datos en un grupo elástico heredarán nivel de servicio de Hola de grupo elástico de hello (Basic, Standard, Premium).</span><span class="sxs-lookup"><span data-stu-id="7e2ad-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="7e2ad-114">Movimiento de una base de datos entre grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="7e2ad-114">Move a database between elastic pools</span></span>
<span data-ttu-id="7e2ad-115">Utilice el comando ALTER DATABASE de hello con hello modificar y establezca servicio\_opción objetiva como ELÁSTICAS\_grupo.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="7e2ad-116">Establecer nombre de grupo de destino de hello toohello de nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="7e2ad-117">Movimiento de una base de datos a un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="7e2ad-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="7e2ad-118">Utilice el comando ALTER DATABASE de hello con hello modificar y establezca servicio\_opción objetiva como ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="7e2ad-119">Establecer nombre de grupo de destino de hello toohello de nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="7e2ad-120">Movimiento de una base de datos fuera de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="7e2ad-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="7e2ad-121">Utilice el comando ALTER DATABASE de Hola y establezca hello SERVICE_OBJECTIVE tooone Hola de niveles de rendimiento (como S0 o S1).</span><span class="sxs-lookup"><span data-stu-id="7e2ad-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="7e2ad-122">Enumeración de bases de datos de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="7e2ad-122">List databases in an elastic pool</span></span>
<span data-ttu-id="7e2ad-123">Hola de uso [sys.database\_servicio \_objetivos vista](https://msdn.microsoft.com/library/mt712619) toolist todos Hola bases de datos de un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="7e2ad-124">Inicie sesión en master toohello vista de base de datos tooquery Hola.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="7e2ad-125">Obtención de datos de uso de recursos para un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="7e2ad-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="7e2ad-126">Hola de uso [sys.elastic\_grupo \_recursos \_ver estadísticas](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine estadísticas de uso de recursos de Hola de un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="7e2ad-127">Inicie sesión en master toohello vista de base de datos tooquery Hola.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="7e2ad-128">Obtención de datos de uso de recursos para una base de datos agrupada</span><span class="sxs-lookup"><span data-stu-id="7e2ad-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="7e2ad-129">Hola de uso [sys.dm\_ db\_ recursos\_ver estadísticas](https://msdn.microsoft.com/library/dn800981.aspx) o [sys.resource \_ver estadísticas](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine estadísticas de uso de recursos de Hola de un base de datos en un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="7e2ad-130">Este proceso es el uso de recursos de tooquerying similar para una sola base de datos.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e2ad-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e2ad-131">Next steps</span></span>
<span data-ttu-id="7e2ad-132">Después de crear un grupo elástico, puede administrar las bases de datos elásticas en grupo de hello mediante la creación de trabajos elásticos.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="7e2ad-133">Trabajos elásticos facilitan la ejecución de scripts de T-SQL con cualquier número de bases de datos en bloque de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="7e2ad-134">Para obtener más información, vea [Información general sobre los trabajos de bases de datos elásticas](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e2ad-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="7e2ad-135">Vea [escalado horizontal con base de datos de SQL Azure](sql-database-elastic-scale-introduction.md): usar bases de datos elásticas herramientas tooscale out, mover los datos, consultar o crear las transacciones.</span><span class="sxs-lookup"><span data-stu-id="7e2ad-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

