---
title: "aaaConfigure replicación geográfica para la base de datos de SQL de Azure con Transact-SQL | Documentos de Microsoft"
description: "Configuración de la replicación geográfica para Azure SQL Database con Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Configuración de la replicación geográfica activa para Azure SQL Database con Transact-SQL

Este artículo muestra cómo tooconfigure replicación geográfica activa para una base de datos de SQL Azure con Transact-SQL.

tooinitiate conmutación por error mediante Transact-SQL, consulte [iniciar una conmutación por error planeada o no planeada de la base de datos de SQL de Azure con Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Cuando se usa la replicación geográfica activa (réplicas secundarias legibles) para la recuperación ante desastres debe configurar un grupo de conmutación por error para todas las bases de datos dentro de una aplicación tooenable automática y transparente conmutación por error. Esta característica se encuentra en su versión preliminar. Para obtener más información, consulte [Grupos de conmutación por error automática y replicación geográfica](sql-database-geo-replication-overview.md).
> 
> 

tooconfigure la replicación geográfica activa mediante Transact-SQL, necesita Hola siguiente:

* Una suscripción de Azure
* Un servidor de base de datos de SQL Azure lógico <MyLocalServer> y una base de datos SQL <MyDB> -Hola base de datos principal que desea tooreplicate
* Hola de servidores de base de datos de SQL Azure lógicos < MySecondaryServer(n) > - uno o varios servidores lógicos que pasarán a ser servidores de socio comercial de hello en el que va a crear bases de datos secundarias
* Un inicio de sesión es DBManager en hello principal
* Tiene db_ownership de hello base de datos local que se va a replicar geográficamente
* Estar DBManager en hello asociado servidores toowhich que va a configurar la replicación geográfica
* versión más reciente de Hola de SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Se recomienda que siempre utilice Hola versión más reciente de Management Studio tooremain sincronizada con actualizaciones tooMicrosoft Azure y base de datos SQL. [Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Agregar una base de datos secundaria
Puede usar hello **ALTER DATABASE** instrucción toocreate una base de datos secundaria a una replicación geográfica en un servidor asociado. Ejecute esta instrucción en base de datos maestra Hola de hello servidor contenedor Hola base de datos toobe replicado. Hello base de datos de replicación geográfica (Hola "base de datos principal") tendrá Hola mismo nombre de base de datos de hello está replicando y que, de forma predeterminada, tienen Hola mismo nivel de servicio como base de datos principal de Hola. Hello base de datos secundaria puede ser legible o ilegible y puede tener una sola base de datos o en un grupo elástico. Para más información, vea [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) y [Niveles de servicio](sql-database-service-tiers.md).
Después de crear y propagado la base de datos secundaria de hello, datos iniciará la réplica de forma asincrónica desde la base de datos principal de Hola. Hola pasos siguientes se describe cómo la replicación geográfica tooconfigure con Management Studio. Se proporcionan pasos toocreate ilegible y legibles elementos secundarios, como una sola base de datos o en un grupo elástico.

> [!NOTE]
> Si existe una base de datos en servidor de socio comercial especificado Hola con hello mismo nombre de comando de Hola de base de datos principal de hello generará un error.
> 

### <a name="add-readable-secondary-single-database"></a>Incorporación de una base de datos secundaria legible (base de datos única)
Usar hello siguiendo los pasos toocreate una secundaria legible como una sola base de datos.

1. En Management Studio, conecte el servidor lógico de tooyour base de datos de SQL Azure.
2. Abra la carpeta de bases de datos de hello, expanda hello **bases de datos de sistema** carpeta, el botón secundario en **maestro**y, a continuación, haga clic en **nueva consulta**.
3. Utilice Hola siguiente **ALTER DATABASE** instrucción toomake una base de datos local en la replicación geográfica principal con una base de datos secundaria legible en un servidor secundario.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Haga clic en **Execute** consulta de hello toorun.

### <a name="add-readable-secondary-elastic-pool"></a>Adición de una base de datos secundaria legible (grupo elástico)
Usar hello siguiendo los pasos toocreate una secundaria legible en un grupo elástico.

1. En Management Studio, conecte el servidor lógico de tooyour base de datos de SQL Azure.
2. Abra la carpeta de bases de datos de hello, expanda hello **bases de datos de sistema** carpeta, el botón secundario en **maestro**y, a continuación, haga clic en **nueva consulta**.
3. Utilice Hola siguiente **ALTER DATABASE** instrucción toomake una base de datos local en la replicación geográfica principal con una base de datos secundaria legible en un servidor secundario en un grupo elástico.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Haga clic en **Execute** consulta de hello toorun.

## <a name="remove-secondary-database"></a>Elimine una base de datos secundaria
Puede usar hello **ALTER DATABASE** instrucción toopermanently Finalizar asociación de replicación de hello entre una base de datos secundaria y su principal. Esta instrucción se ejecuta en hello base de datos maestra en qué Hola reside la base de datos principal. Tras la terminación de la relación de hello, base de datos secundaria de Hola se convierte en una base de datos de lectura y escritura normal. Si se interrumpe la base de datos de toosecondary de conectividad de Hola Hola comando se ejecuta correctamente pero Hola secundaria se convertirá en lectura y escritura después de que se restaure la conectividad. Para más información, vea [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) y [Niveles de servicio](sql-database-service-tiers.md).

Usar hello siguiendo los pasos tooremove georreplicadas base de datos secundaria de un perfil de replicación geográfica.

1. En Management Studio, conecte el servidor lógico de tooyour base de datos de SQL Azure.
2. Abra la carpeta de bases de datos de hello, expanda hello **bases de datos de sistema** carpeta, el botón secundario en **maestro**y, a continuación, haga clic en **nueva consulta**.
3. Utilice Hola siguiente **ALTER DATABASE** secundaria tooremove replicación geográfica de instrucción.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Haga clic en **Execute** consulta de hello toorun.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Supervisión y mantenimiento de la configuración de la replicación geográfica activa

Tareas de supervisión incluyen la supervisión de configuración de replicación geográfica de Hola y supervisar el estado de replicación de datos.  Puede usar hello **sys.dm_geo_replication_links** vista de administración dinámica en hello base de datos maestra tooreturn saber todos los vínculos de replicación existente para cada base de datos en el servidor lógico de base de datos de SQL Azure de Hola. Esta vista contiene una fila para cada vínculo de replicación de hello entre bases de datos principales y secundarias. Puede usar hello **sys.dm_replication_link_status** vista de administración dinámica tooreturn una fila para cada base de datos de SQL Azure que participa en un vínculo de replicación de replicación. Aquí se incluyen tanto las bases de datos principales como secundarias. Si existe más de un vínculo de replicación continua para una base de datos principal, esta tabla contiene una fila para cada una de las relaciones de Hola. se crea la vista de Hello en todas las bases de datos, incluida la maestra lógica Hola. Sin embargo, al consultar esta vista en maestra lógica hello, devuelve un conjunto vacío. Puede usar hello **sys.dm_operation_status** tooshow estado de saludo de la vista de administración dinámica para todas las operaciones, incluido el estado de Hola Hola vínculos de replicación de base de datos. Para más información, consulte [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) y [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).

Usar hello después de asociación de toomonitor una replicación geográfica activa de pasos.

1. En Management Studio, conecte el servidor lógico de tooyour base de datos de SQL Azure.
2. Abra la carpeta de bases de datos de hello, expanda hello **bases de datos de sistema** carpeta, el botón secundario en **maestro**y, a continuación, haga clic en **nueva consulta**.
3. Usar hello después de la instrucción tooshow todas las bases de datos con vínculos de replicación geográfica.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Haga clic en **Execute** consulta de hello toorun.
5. Abra la carpeta de bases de datos de hello, expanda hello **bases de datos de sistema** carpeta, el botón secundario en **MyDB**y, a continuación, haga clic en **nueva consulta**.
6. Hola de uso después de la replicación de instrucción tooshow Hola se queda atrás y última hora de la replicación de mis bases de datos secundarias de MyDB.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Haga clic en **Execute** consulta de hello toorun.
8. Usar hello siguientes instrucción tooshow hello más reciente replicación geográfica operaciones asociadas con la base de datos MyDB.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Haga clic en **Execute** consulta de hello toorun.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de los grupos de conmutación por error y replicación geográfica activa, vea - [grupos de conmutación por error](sql-database-geo-replication-overview.md)
* Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Continuidad empresarial con Base de datos SQL de Azure](sql-database-business-continuity.md)

