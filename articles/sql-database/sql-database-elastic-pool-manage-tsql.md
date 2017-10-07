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
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Supervisión y administración de un grupo elástico con Transact-SQL
Este tema muestra cómo toomanage escalable [grupos elásticos](sql-database-elastic-pool.md) con Transact-SQL.  También puede crear y administrar un hello Azure grupo elástico [portal de Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), API de REST de Hola o [C#](sql-database-elastic-pool-manage-csharp.md). También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Hola de uso [Create Database (base de datos de SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) y [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) comandos toocreate y mover bases de datos dentro y fuera de grupos elásticos. grupo elástico Hola debe existir para poder utilizar estos comandos. Estos comandos afectan solo a las bases de datos. Creación de grupos nuevos y Hola establecer propiedades de grupo (por ejemplo, min y max Edtu) no se puede cambiar con comandos de T-SQL.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Creación de una base de datos agrupada en un grupo elástico
Usar el comando CREATE DATABASE de Hola con Hola opción SERVICE_OBJECTIVE.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Todas las bases de datos en un grupo elástico heredarán nivel de servicio de Hola de grupo elástico de hello (Basic, Standard, Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Movimiento de una base de datos entre grupos elásticos
Utilice el comando ALTER DATABASE de hello con hello modificar y establezca servicio\_opción objetiva como ELÁSTICAS\_grupo. Establecer nombre de grupo de destino de hello toohello de nombre de Hola.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Movimiento de una base de datos a un grupo elástico
Utilice el comando ALTER DATABASE de hello con hello modificar y establezca servicio\_opción objetiva como ELASTIC_POOL. Establecer nombre de grupo de destino de hello toohello de nombre de Hola.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Movimiento de una base de datos fuera de un grupo elástico
Utilice el comando ALTER DATABASE de Hola y establezca hello SERVICE_OBJECTIVE tooone Hola de niveles de rendimiento (como S0 o S1).

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Enumeración de bases de datos de un grupo elástico
Hola de uso [sys.database\_servicio \_objetivos vista](https://msdn.microsoft.com/library/mt712619) toolist todos Hola bases de datos de un grupo elástico. Inicie sesión en master toohello vista de base de datos tooquery Hola.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Obtención de datos de uso de recursos para un grupo elástico
Hola de uso [sys.elastic\_grupo \_recursos \_ver estadísticas](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine estadísticas de uso de recursos de Hola de un grupo elástico en un servidor lógico. Inicie sesión en master toohello vista de base de datos tooquery Hola.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Obtención de datos de uso de recursos para una base de datos agrupada
Hola de uso [sys.dm\_ db\_ recursos\_ver estadísticas](https://msdn.microsoft.com/library/dn800981.aspx) o [sys.resource \_ver estadísticas](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine estadísticas de uso de recursos de Hola de un base de datos en un grupo elástico. Este proceso es el uso de recursos de tooquerying similar para una sola base de datos.

## <a name="next-steps"></a>Pasos siguientes
Después de crear un grupo elástico, puede administrar las bases de datos elásticas en grupo de hello mediante la creación de trabajos elásticos. Trabajos elásticos facilitan la ejecución de scripts de T-SQL con cualquier número de bases de datos en bloque de Hola. Para obtener más información, vea [Información general sobre los trabajos de bases de datos elásticas](sql-database-elastic-jobs-overview.md). 

Vea [escalado horizontal con base de datos de SQL Azure](sql-database-elastic-scale-introduction.md): usar bases de datos elásticas herramientas tooscale out, mover los datos, consultar o crear las transacciones.

