---
title: "T-SQL: Administración de un grupo elástico de Azure SQL Database | Microsoft Docs"
description: "Use T-SQL para administrar un grupo elástico de Azure SQL Database."
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
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="17053-103">Supervisión y administración de un grupo elástico con Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="17053-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="17053-104">En este tema se muestra cómo administrar [grupos elásticos](sql-database-elastic-pool.md) escalables con Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="17053-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="17053-105">También puede crear y administrar un grupo elástico de Azure en [Azure Portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), la API de REST o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="17053-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="17053-106">También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="17053-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="17053-107">Utilice los comandos [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) y [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) para crear e introducir y sacar las bases de datos de los grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="17053-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="17053-108">El grupo elástico debe existir antes de poder utilizar estos comandos.</span><span class="sxs-lookup"><span data-stu-id="17053-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="17053-109">Estos comandos afectan solo a las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="17053-109">These commands affect only databases.</span></span> <span data-ttu-id="17053-110">La creación de nuevos grupos y la configuración de las propiedades de grupo (por ejemplo, de los valores mín. y máx. de eDTU) no se puede cambiar mediante comandos de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="17053-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="17053-111">Creación de una base de datos agrupada en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="17053-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="17053-112">Use el comando CREATE DATABASE con la opción SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="17053-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="17053-113">Todas las bases de datos de un grupo elástico heredan el nivel de servicio del grupo elástico (Básico, Estándar, Premium).</span><span class="sxs-lookup"><span data-stu-id="17053-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="17053-114">Movimiento de una base de datos entre grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="17053-114">Move a database between elastic pools</span></span>
<span data-ttu-id="17053-115">Utilice el comando ALTER DATABASE con MODIFY y configure la opción SERVICE\_OBJECTIVE como ELASTIC\_POOL.</span><span class="sxs-lookup"><span data-stu-id="17053-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="17053-116">Establezca como nombre el nombre del grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="17053-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="17053-117">Movimiento de una base de datos a un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="17053-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="17053-118">Utilice el comando ALTER DATABASE con MODIFY y configure la opción SERVICE\_OBJECTIVE como ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="17053-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="17053-119">Establezca como nombre el nombre del grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="17053-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="17053-120">Movimiento de una base de datos fuera de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="17053-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="17053-121">Utilice el comando ALTER DATABASE y establezca SERVICE_OBJECTIVE en uno de los niveles de rendimiento (como S0 o S1).</span><span class="sxs-lookup"><span data-stu-id="17053-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="17053-122">Enumeración de bases de datos de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="17053-122">List databases in an elastic pool</span></span>
<span data-ttu-id="17053-123">Utilice la vista [sys.database\_service\_objectives](https://msdn.microsoft.com/library/mt712619) para enumerar todas las bases de datos de un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="17053-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="17053-124">Inicie sesión en la base de datos maestra para efectuar una consulta en la vista.</span><span class="sxs-lookup"><span data-stu-id="17053-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="17053-125">Obtención de datos de uso de recursos para un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="17053-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="17053-126">Utilice la vista [sys.elastic\_pool\_resource\_stats](https://msdn.microsoft.com/library/mt280062.aspx) para examinar las estadísticas de uso de los recursos de un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="17053-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="17053-127">Inicie sesión en la base de datos maestra para efectuar una consulta en la vista.</span><span class="sxs-lookup"><span data-stu-id="17053-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="17053-128">Obtención de datos de uso de recursos para una base de datos agrupada</span><span class="sxs-lookup"><span data-stu-id="17053-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="17053-129">Utilice la vista [sys.dm\_db\_resource\_stats](https://msdn.microsoft.com/library/dn800981.aspx) o la vista [sys.resource\_stats](https://msdn.microsoft.com/library/dn269979.aspx) para examinar las estadísticas de uso de los recursos de una base de datos en un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="17053-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="17053-130">Este proceso es similar a la consulta de uso de recursos para una base de datos única.</span><span class="sxs-lookup"><span data-stu-id="17053-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17053-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17053-131">Next steps</span></span>
<span data-ttu-id="17053-132">Tras la creación de un grupo elástico, puede administrar las bases de datos elásticas del grupo mediante la creación de trabajos elásticos.</span><span class="sxs-lookup"><span data-stu-id="17053-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="17053-133">Los trabajos elásticos facilitan la ejecución de secuencias de comandos de T-SQL con cualquier número de bases de datos en el grupo.</span><span class="sxs-lookup"><span data-stu-id="17053-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="17053-134">Para obtener más información, vea [Información general sobre los trabajos de bases de datos elásticas](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17053-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="17053-135">Consulte [Escalado horizontal con Azure SQL Database](sql-database-elastic-scale-introduction.md): use herramientas de bases de datos elásticas para realizar un escalado horizontal, mover los datos, realizar consultas o crear transacciones.</span><span class="sxs-lookup"><span data-stu-id="17053-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

