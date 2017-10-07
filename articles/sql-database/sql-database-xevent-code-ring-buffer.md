---
title: "aaaXEvent código de búfer en anillo para la base de datos SQL | Documentos de Microsoft"
description: "Proporciona un ejemplo de código de Transact-SQL que se realiza la forma más fácil y rápido mediante el uso del destino de búfer de anillo de hello, en la base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>Código de destino de búfer de anillo para eventos extendidos en Base de datos SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Un ejemplo de código completo que desea para hello más fácil forma rápida toocapture y notificar información para un evento extendido durante una prueba. destino de más fácil de Hola para datos de eventos extendidos es hello [destino de búfer de anillo](http://msdn.microsoft.com/library/ff878182.aspx).

En este tema, se presenta un ejemplo de código de Transact-SQL que:

1. Crea una tabla con datos toodemonstrate con.
2. Crea una sesión para un evento extendido existente, es decir, **sqlserver.sql_statement_starting**.
   
   * evento Hello es limitado tooSQL instrucciones que contienen una determinada cadena de actualización: **instrucción LIKE '% actualización tabEmployee %'**.
   * Elige la salida de hello toosend hello tooa del destino de evento de tipo de búfer de anillo, a saber **package0.ring_buffer**.
3. Inicia la sesión de eventos de Hola.
4. Emite un par de instrucciones SQL UPDATE simple.
5. Emite una instrucción SELECT de SQL, tooretrieve salida de eventos de hello búfer de anillo.
   
   * Se unen **sys.dm_xe_database_session_targets** y otras vistas de administración dinámica (DMV).
6. Detiene la sesión de eventos de Hola.
7. Quita Hola destino de búfer en anillo, toorelease sus recursos.
8. Quita la sesión de eventos de Hola y tabla de demostración de hello.

## <a name="prerequisites"></a>Requisitos previos

* Una cuenta y una suscripción de Azure. Puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Cualquier base de datos donde pueda crear una tabla.
  
  * De manera opcional, puede [crear una base de datos de **AdventureWorksLT** de demostración](sql-database-get-started.md) en cuestión de minutos.
* SQL Server Management Studio (ssms.exe), idealmente la versión de actualización mensual más reciente. 
  Puede descargar hello ssms.exe más reciente desde:
  
  * El tema titulado [Descarga de SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Una descarga de toohello vínculo directo.](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>Código de ejemplo

Con muy pequeñas modificaciones, hello siguiente ejemplo de código de búfer de anillo puede realizarse en la base de datos de SQL Azure o Microsoft SQL Server. diferencia de Hello es la presencia de hello del nodo de hello '_Base de datos' en nombre de Hola de algunas vistas de administración dinámica (DMV), utilizado en la cláusula FROM de hello en el paso 5. Por ejemplo:

* sys.dm_xe**_database**_session_targets
* sys.dm_xe_session_targets

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a>Contenido del Búfer de anillo

Se utiliza el ejemplo de código de hello toorun ssms.exe.

resultados de hello tooview, se hace clic en celda hello en el encabezado de columna de hello **target_data_XML**.

A continuación, en panel de resultados de Hola se hace clic en celda hello en el encabezado de columna de hello **target_data_XML**. Haga clic en crear otra pestaña de archivo en ssms.exe en qué Hola se mostró el contenido de la celda de resultado de hello, como XML.

se muestra el resultado de Hello en hello detrás bloque. Parece largo, pero son solo dos elementos **<event>** .

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a>Liberar los recursos contenidos en el Búfer de anillo

Cuando haya terminado con el búfer de anillo, puede quitarlo y liberar sus recursos emitir un **ALTER** que Hola siguiente:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


definición de Hello de la sesión de eventos se actualiza, pero no se quitan. Más adelante, puede agregar otra instancia de la sesión de eventos de tooyour de búfer en anillo de hello:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>Más información

Hola tema principal para eventos extendidos en base de datos de SQL Azure es:

* [Consideraciones de eventos extendidos en Base de datos SQL](sql-database-xevent-db-diff-from-svr.md), que compara algunos aspectos de los eventos extendidos que son distintos entre Base de datos SQL de Azure y Microsoft SQL Server.

Otros temas de ejemplo de código para eventos extendidos están disponibles en los siguientes vínculos de Hola. Sin embargo, debe comprobar con regularidad cualquier toosee ejemplo si el ejemplo hello tiene como destino de Microsoft SQL Server frente a la base de datos de SQL Azure. A continuación, puede decidir si cambios menores son ejemplo de Hola a toorun necesarios.

* Ejemplo de código para Base de datos SQL de Azure: [Código de destino del archivo de evento para eventos extendidos en Base de datos SQL](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
