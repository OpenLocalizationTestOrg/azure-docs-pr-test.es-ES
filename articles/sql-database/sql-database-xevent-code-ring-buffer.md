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
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="f4920-103">Código de destino de búfer de anillo para eventos extendidos en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f4920-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="f4920-104">Un ejemplo de código completo que desea para hello más fácil forma rápida toocapture y notificar información para un evento extendido durante una prueba.</span><span class="sxs-lookup"><span data-stu-id="f4920-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="f4920-105">destino de más fácil de Hola para datos de eventos extendidos es hello [destino de búfer de anillo](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4920-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="f4920-106">En este tema, se presenta un ejemplo de código de Transact-SQL que:</span><span class="sxs-lookup"><span data-stu-id="f4920-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="f4920-107">Crea una tabla con datos toodemonstrate con.</span><span class="sxs-lookup"><span data-stu-id="f4920-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="f4920-108">Crea una sesión para un evento extendido existente, es decir, **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="f4920-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="f4920-109">evento Hello es limitado tooSQL instrucciones que contienen una determinada cadena de actualización: **instrucción LIKE '% actualización tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="f4920-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="f4920-110">Elige la salida de hello toosend hello tooa del destino de evento de tipo de búfer de anillo, a saber **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="f4920-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="f4920-111">Inicia la sesión de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4920-111">Starts hello event session.</span></span>
4. <span data-ttu-id="f4920-112">Emite un par de instrucciones SQL UPDATE simple.</span><span class="sxs-lookup"><span data-stu-id="f4920-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="f4920-113">Emite una instrucción SELECT de SQL, tooretrieve salida de eventos de hello búfer de anillo.</span><span class="sxs-lookup"><span data-stu-id="f4920-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="f4920-114">Se unen **sys.dm_xe_database_session_targets** y otras vistas de administración dinámica (DMV).</span><span class="sxs-lookup"><span data-stu-id="f4920-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="f4920-115">Detiene la sesión de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4920-115">Stops hello event session.</span></span>
7. <span data-ttu-id="f4920-116">Quita Hola destino de búfer en anillo, toorelease sus recursos.</span><span class="sxs-lookup"><span data-stu-id="f4920-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="f4920-117">Quita la sesión de eventos de Hola y tabla de demostración de hello.</span><span class="sxs-lookup"><span data-stu-id="f4920-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4920-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f4920-118">Prerequisites</span></span>

* <span data-ttu-id="f4920-119">Una cuenta y una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4920-119">An Azure account and subscription.</span></span> <span data-ttu-id="f4920-120">Puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4920-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f4920-121">Cualquier base de datos donde pueda crear una tabla.</span><span class="sxs-lookup"><span data-stu-id="f4920-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="f4920-122">De manera opcional, puede [crear una base de datos de **AdventureWorksLT** de demostración](sql-database-get-started.md) en cuestión de minutos.</span><span class="sxs-lookup"><span data-stu-id="f4920-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="f4920-123">SQL Server Management Studio (ssms.exe), idealmente la versión de actualización mensual más reciente.</span><span class="sxs-lookup"><span data-stu-id="f4920-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="f4920-124">Puede descargar hello ssms.exe más reciente desde:</span><span class="sxs-lookup"><span data-stu-id="f4920-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="f4920-125">El tema titulado [Descarga de SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4920-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="f4920-126">Una descarga de toohello vínculo directo.</span><span class="sxs-lookup"><span data-stu-id="f4920-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="f4920-127">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4920-127">Code sample</span></span>

<span data-ttu-id="f4920-128">Con muy pequeñas modificaciones, hello siguiente ejemplo de código de búfer de anillo puede realizarse en la base de datos de SQL Azure o Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4920-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="f4920-129">diferencia de Hello es la presencia de hello del nodo de hello '_Base de datos' en nombre de Hola de algunas vistas de administración dinámica (DMV), utilizado en la cláusula FROM de hello en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="f4920-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="f4920-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f4920-130">For example:</span></span>

* <span data-ttu-id="f4920-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="f4920-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="f4920-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="f4920-132">sys.dm_xe_session_targets</span></span>

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

## <a name="ring-buffer-contents"></a><span data-ttu-id="f4920-133">Contenido del Búfer de anillo</span><span class="sxs-lookup"><span data-stu-id="f4920-133">Ring Buffer contents</span></span>

<span data-ttu-id="f4920-134">Se utiliza el ejemplo de código de hello toorun ssms.exe.</span><span class="sxs-lookup"><span data-stu-id="f4920-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="f4920-135">resultados de hello tooview, se hace clic en celda hello en el encabezado de columna de hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="f4920-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="f4920-136">A continuación, en panel de resultados de Hola se hace clic en celda hello en el encabezado de columna de hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="f4920-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="f4920-137">Haga clic en crear otra pestaña de archivo en ssms.exe en qué Hola se mostró el contenido de la celda de resultado de hello, como XML.</span><span class="sxs-lookup"><span data-stu-id="f4920-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="f4920-138">se muestra el resultado de Hello en hello detrás bloque.</span><span class="sxs-lookup"><span data-stu-id="f4920-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="f4920-139">Parece largo, pero son solo dos elementos **<event>** .</span><span class="sxs-lookup"><span data-stu-id="f4920-139">It looks long, but it is just two **<event>** elements.</span></span>

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


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="f4920-140">Liberar los recursos contenidos en el Búfer de anillo</span><span class="sxs-lookup"><span data-stu-id="f4920-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="f4920-141">Cuando haya terminado con el búfer de anillo, puede quitarlo y liberar sus recursos emitir un **ALTER** que Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4920-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="f4920-142">definición de Hello de la sesión de eventos se actualiza, pero no se quitan.</span><span class="sxs-lookup"><span data-stu-id="f4920-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="f4920-143">Más adelante, puede agregar otra instancia de la sesión de eventos de tooyour de búfer en anillo de hello:</span><span class="sxs-lookup"><span data-stu-id="f4920-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="f4920-144">Más información</span><span class="sxs-lookup"><span data-stu-id="f4920-144">More information</span></span>

<span data-ttu-id="f4920-145">Hola tema principal para eventos extendidos en base de datos de SQL Azure es:</span><span class="sxs-lookup"><span data-stu-id="f4920-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="f4920-146">[Consideraciones de eventos extendidos en Base de datos SQL](sql-database-xevent-db-diff-from-svr.md), que compara algunos aspectos de los eventos extendidos que son distintos entre Base de datos SQL de Azure y Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4920-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="f4920-147">Otros temas de ejemplo de código para eventos extendidos están disponibles en los siguientes vínculos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4920-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="f4920-148">Sin embargo, debe comprobar con regularidad cualquier toosee ejemplo si el ejemplo hello tiene como destino de Microsoft SQL Server frente a la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f4920-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="f4920-149">A continuación, puede decidir si cambios menores son ejemplo de Hola a toorun necesarios.</span><span class="sxs-lookup"><span data-stu-id="f4920-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="f4920-150">Ejemplo de código para Base de datos SQL de Azure: [Código de destino del archivo de evento para eventos extendidos en Base de datos SQL](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="f4920-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
