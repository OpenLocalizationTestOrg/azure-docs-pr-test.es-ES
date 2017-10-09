---
title: "aaaManage los datos históricos en las tablas temporales con directiva de retención | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse retención temporal directiva tookeep datos históricos bajo su control."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Administración de datos históricos en tablas temporales con directivas de retención
Las tablas temporales pueden aumentar el tamaño de la base de datos más que las tablas normales, especialmente si conserva datos históricos durante un período de tiempo más largo. Por lo tanto, la directiva de retención para datos históricos es un aspecto importante de planeación y la administración del ciclo de vida de Hola de cada tabla temporal. Las tablas temporales de Azure SQL Database incluyen un mecanismo de retención fácil de usar que ayuda a realizar esta tarea.

Retención de historial temporal puede configurarse en el nivel de tabla individuales de hello, que permite a los usuarios las directivas de caducidad flexible toocreate. Aplicar la retención temporal es simple: requiere un único toobe parámetro establecido durante el cambio de esquema o de creación de tabla.

Después de definir la directiva de retención, Azure SQL Database comenzará a comprobar periódicamente si hay filas históricas que son aptas para la limpieza automática de datos. Identificación de las filas coincidentes y su eliminación de la tabla de historial de Hola se producen de forma transparente, en la tarea en segundo plano Hola programado y ejecutado por el sistema de Hola. Se comprueba la condición de edad para las filas de tabla de historial de hello en función de la columna de Hola que representa el final del período de SYSTEM_TIME. Si el período de retención, por ejemplo, se establece toosix en meses, filas aptas para la limpieza de la tabla satisfacen Hola siguiente condición:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

En el anterior ejemplo de Hola, asumimos que **ValidTo** columna corresponde toohello final del período de SYSTEM_TIME.

## <a name="how-tooconfigure-retention-policy"></a>¿La directiva de retención de tooconfigure?
Antes de configurar la directiva de retención para una tabla temporal, primero compruebe si está habilitada la retención de historial temporal *en el nivel de base de datos de hello*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Marca la base de datos **is_temporal_history_retention_enabled** es tooON de conjunto de forma predeterminada, pero los usuarios pueden cambiar con la instrucción ALTER DATABASE. También es automáticamente set tooOFF después [punto de restauración a un momento](sql-database-recovery-using-backups.md) operación. tooenable la limpieza de la retención de historial temporal para la base de datos, ejecute hello siguiente instrucción:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> Puede configurar la retención para tablas temporales aunque **is_temporal_history_retention_enabled** esté establecida en OFF, pero en ese caso no se desencadenará la limpieza automática de las filas de datos antiguos.
> 
> 

Directiva de retención se configura durante la creación de una tabla especificando el valor de parámetro de hello HISTORY_RETENTION_PERIOD:

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

La base de datos de SQL Azure le permite toospecify período de retención mediante el uso de unidades de tiempo diferentes: días, semanas, meses y años. Si se omite HISTORY_RETENTION_PERIOD, se supone una retención INFINITA. También puede usar explícitamente la palabra clave INFINITO.

En algunos escenarios, puede que desee tooconfigure retención después de la creación de una tabla o toochange valor configurado previamente. En ese caso use la instrucción ALTER TABLE:

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> Establecer SYSTEM_VERSIONING tooOFF *no conserva* valor de período de retención. Establecer SYSTEM_VERSIONING tooON sin HISTORY_RETENTION_PERIOD especifica explícitamente resultados en el período de retención INFINITA de Hola.
> 
> 

tooreview el estado actual de la directiva de retención de hello, uso siguiente de hello consulta dicha marca de habilitación de retención temporal de combinaciones en el nivel de base de datos de hello con períodos de retención para tablas individuales:

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a>¿Cómo SQL Database elimina las filas antiguas?
proceso de limpieza de Hello depende de diseño del índice de Hola de tabla de historial de Hola. Es importante toonotice que *sólo tablas de historial con un índice agrupado (árbol B o almacén de columnas) pueden tener una directiva de retención finito configurado*. Una tarea en segundo plano se crea tooperform de limpieza de datos antiguos para todas las tablas temporales con el período de retención finito.
Lógica de limpieza para el índice agrupado de almacén de filas (árbol B) Hola elimina la fila antigua en fragmentos más pequeños (arriba too10K) minimizar la presión en el registro de base de datos y el subsistema de E/S. A pesar de que utiliza la lógica de limpieza necesarias índice de árbol B, orden de las eliminaciones de filas de hello antigüedad mayor que el período de retención no se puede garantizar bien. Por lo tanto, *no tienen ninguna dependencia en el orden de limpieza de hello en sus aplicaciones*.

Hello tarea limpieza de hello en clúster de almacén de columnas quita todo [grupos de filas](https://msdn.microsoft.com/library/gg492088.aspx) a la vez (normalmente contiene 1 millón de filas cada uno), que es muy eficaz, especialmente cuando los datos históricos se generan a un ritmo alta.

![Retención de almacén de columnas agrupado](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

La excelente compresión de datos y la eficaz limpieza de retención convierten al índice del almacén de columnas agrupado en una perfecta opción en escenarios en los que la carga de trabajo genera rápidamente gran cantidad de datos históricos. Este patrón es típico de [cargas de trabajo intensivas de procesamiento de transacciones que usan tablas temporales](https://msdn.microsoft.com/library/mt631669.aspx) para el seguimiento de cambios y la auditoría, el análisis de tendencias o la ingesta de datos de IoT.

## <a name="index-considerations"></a>Consideraciones sobre el índice
tarea de limpieza de Hello para las tablas con índice agrupado de almacén requiere toostart de índice con finales Hola Hola columna correspondientes de periodo SYSTEM_TIME. Si este tipo de índice no existe, no se puede configurar un periodo de retención finito:

*Msg 13765, nivel 16, estado 1 <br> </br> período de retención finito no se pudo establecer en la tabla temporal con versión del sistema 'temporalstagetestdb.dbo.WebsiteUserInfo' porque la tabla de historial de hello ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' no contiene el índice clúster necesaria. Considere la posibilidad de crear un almacén de columnas agrupado o un índice de árbol B a partir de columna de Hola que coincide con el final de SYSTEM_TIME period, en la tabla de historial de Hola.*

Es importante toonotice que Hola tabla de historial de predeterminada creada por base de datos de SQL Azure ya tiene el índice, que es compatible con directiva de retención de clúster. Si intentas tooremove ese índice en una tabla con el período de retención finito, se produce un error en la operación con hello siguiente error:

*Msg 13766, nivel 16, estado 1 <br> </br> no se puede quitar el índice agrupado de hello 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' porque está siendo utilizado para la limpieza automática de los datos antiguos. Considere la posibilidad de configuración HISTORY_RETENTION_PERIOD tooINFINITE en tabla temporal con versión del sistema correspondiente Hola si necesita toodrop este índice.*

Liberador de espacio en el índice de almacén de columnas agrupado Hola funcione de manera óptima si se insertan filas históricas en orden ascendente (ordenado por final Hola de columna de período), que siempre es el caso de hello cuando se rellena la tabla de historial de hello exclusivamente por hello SYSTEM_ de Hola Mecanismo VERSIONIOING. Si no se ordenan filas de tabla de historial de hello al final de la columna de periodo (que puede ser el caso de hello si ha migrado los datos históricos existentes), debe volver a crear índice de almacén de columnas agrupado sobre el índice de almacén de filas de árbol B que está ordenado correctamente, tooachieve óptimo rendimiento.

Evitar volver a generar índice de almacén de columnas agrupado en la tabla de historial de hello con período de retención finita de hello, ya que puede cambiar la ordenación en grupos de filas de hello naturalmente impuestos por la operación de control de versiones de Hola. Si necesita toorebuild índice de almacén de columnas agrupado en la tabla de historial de hello, hágalo por volver a crearla en la parte superior compatible con índice de árbol B, conserva la ordenación en grupos de filas de hello necesarios para la limpieza de datos normal. Hola mismo enfoque debe realizarse si crear tabla temporal con tabla de historial existente que tiene el índice de columna sin orden de datos garantizada clúster:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

Cuando el período de retención finito está configurado para la tabla de historial de hello con índice de almacén de columnas agrupado hello, no se puede crear otros índices de árbol B no agrupado en la tabla:

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Se produce un error en un tooexecute intento por encima de la instrucción con hello siguiente error:

*Mens. 13772, Nivel 16, Estado 1 <br></br> No se puede crear un índice no agrupado en la tabla de historial temporal 'WebsiteUserInfoHistory' porque tiene definido un período de retención finito y un índice agrupado de almacén de columnas.*

## <a name="querying-tables-with-retention-policy"></a>Consulta de tablas con directiva de retención
Todas las consultas en una tabla temporal Hola filtran automáticamente históricas filas que coinciden con directiva de retención finito, tooavoid resultados impredecibles e incoherentes, ya que se pueden eliminar filas antiguos por la tarea de limpieza de hello, *en cualquier momento en el tiempo y en orden arbitrario*.

Hello siguiente imagen muestra hello plan de consulta para una consulta simple:

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

consulta de Hello plan incluye filtro adicional aplica tooend de columna de periodo (ValidTo) in Hola Clustered Index Scan (operador) en la tabla de historial de hello (resaltada). En este ejemplo se supone que se ha establecido el período de retención de 1 MES en la tabla WebsiteUserInfo.

![Filtro de consulta de retención](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

Sin embargo, si consulta la tabla de historial directamente, puede ver filas con una antigüedad mayor que el período de retención especificado, pero sin garantía de resultados de consulta repetibles. Hello siguiente imagen muestra plan de ejecución de consulta para consultas de hello en la tabla de historial de hello sin aplicar los filtros adicionales:

![Consulta del historial sin filtro de retención](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

No se fíe de la lógica empresarial al leer la tabla de historial más allá del período de retención, ya que puede obtener resultados inesperados o incoherentes. Se recomienda usar consultas temporales con la cláusula FOR SYSTEM_TIME para analizar los datos de tablas temporales.

## <a name="point-in-time-restore-considerations"></a>Consideraciones sobre la restauración a un momento dado
Cuando se crea la nueva base de datos por [restauración punto específico de tooa de base de datos existente en el tiempo](sql-database-recovery-using-backups.md), tiene retención temporal deshabilitada en el nivel de base de datos de Hola. (**is_temporal_history_retention_enabled** marca establece tooOFF). Esta funcionalidad le permite tooexamine todas las filas históricas durante la restauración, sin tener en cuenta que antiguos filas se quitan antes de obtener tooquery ellos. Puede usar demasiado*inspeccionar los datos históricos más allá del período de retención configurado*.

Supongamos que una tabla temporal tiene especificado un período de retención de un MES. Si la base de datos se creó en el nivel de servicio Premium, sería toocreate capaz de copia de base de datos con el estado de base de datos de hello días laborables too35 en hello anterior. Que eficazmente permitiría tooanalyze filas históricos que están funcionando too65 días de antigüedad consultando la tabla de historial de hello directamente.

Si desea que la limpieza de la retención temporal tooactivate, ejecute hello después de la instrucción de Transact-SQL después de punto de restauración a un momento dado:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Pasos siguientes
cómo desproteger toouse las tablas temporales de las aplicaciones de toolearn [Introducción a las tablas temporales de base de datos de SQL Azure](sql-database-temporal-tables.md).

Visita Channel 9 toohear una [historia de éxito de clientes reales implementación temporal](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) inspección y un [live temporal demostración](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Para más información sobre las tablas temporales, revise la [documentación de MSDN](https://msdn.microsoft.com/library/dn935015.aspx).

