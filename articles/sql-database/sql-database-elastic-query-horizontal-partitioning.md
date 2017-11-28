---
title: aaaReporting entre bases de datos de escala horizontal en la nube | Documentos de Microsoft
description: "¿Cómo tooset elástico consultas en particiones horizontales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="473ce-103">Informes de bases de datos escaladas horizontalmente en la nube (vista previa)</span><span class="sxs-lookup"><span data-stu-id="473ce-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Consultas entre particiones][1]

<span data-ttu-id="473ce-105">Filas de distribución de bases de datos particionadas en un nivel de datos escalado horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="473ce-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="473ce-106">esquema de Hello es idéntica en todas las bases de datos participantes, que también se conoce como creación de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="473ce-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="473ce-107">Utilice una consulta elástica para crear informes que abarquen todas las bases de datos en una base de datos particionada.</span><span class="sxs-lookup"><span data-stu-id="473ce-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="473ce-108">Para un inicio rápido, consulte [Informes de bases de datos escaladas horizontalmente en la nube](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="473ce-109">Para bases de datos no particionadas, consulte [Consulta de bases de datos elásticas para consultas entre bases de datos (particionamiento vertical)](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="473ce-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="473ce-110">Prerequisites</span></span>
* <span data-ttu-id="473ce-111">Crear un mapa de particiones mediante la biblioteca de cliente de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="473ce-112">Consulte [Administración de asignaciones particionadas](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="473ce-113">O use la aplicación de ejemplo de Hola en [empezar a trabajar con herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="473ce-114">Como alternativa, vea [existente migrar bases de datos de las bases de datos fuera de tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="473ce-115">usuario de Hello debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="473ce-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="473ce-116">Este permiso se incluye con el permiso ALTER DATABASE Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="473ce-117">Los permisos ALTER ANY EXTERNAL DATA SOURCE son toohello toorefer necesario el origen de datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="473ce-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="473ce-118">Información general</span><span class="sxs-lookup"><span data-stu-id="473ce-118">Overview</span></span>
<span data-ttu-id="473ce-119">Estas instrucciones crean representación de metadatos de hello de la capa de datos particionada en base de datos de consulta flexible de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="473ce-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="473ce-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="473ce-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="473ce-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="473ce-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="473ce-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="473ce-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="473ce-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="473ce-124">1.1 Creación de clave maestra y credenciales con ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="473ce-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="473ce-125">se utiliza la credencial de Hola Hola consulta elástico tooconnect tooyour remoto las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="473ce-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="473ce-126">Asegúrese de que ese hello *"\<nombre de usuario\>"* no incluye ningún *"@servername"* sufijo.</span><span class="sxs-lookup"><span data-stu-id="473ce-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="473ce-127">1.2 Creación de orígenes de datos externos</span><span class="sxs-lookup"><span data-stu-id="473ce-127">1.2 Create external data sources</span></span>
<span data-ttu-id="473ce-128">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="473ce-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="473ce-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="473ce-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="473ce-130">Recuperar la lista de hello actual orígenes de datos externos:</span><span class="sxs-lookup"><span data-stu-id="473ce-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="473ce-131">origen de datos externo de Hello hace referencia a la asignación de particiones.</span><span class="sxs-lookup"><span data-stu-id="473ce-131">hello external data source references your shard map.</span></span> <span data-ttu-id="473ce-132">Una consulta flexible, a continuación, usa hello subyacente particiones tooenumerate hello las bases de datos que participan en la capa de datos de Hola y origen de datos externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="473ce-133">Hello mismas credenciales son mapa de particiones de hello tooread usado y tooaccess Hola datos en particiones de Hola durante el procesamiento de Hola de una consulta flexible.</span><span class="sxs-lookup"><span data-stu-id="473ce-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="473ce-134">1.3 Creación de tablas externas</span><span class="sxs-lookup"><span data-stu-id="473ce-134">1.3 Create external tables</span></span>
<span data-ttu-id="473ce-135">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="473ce-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="473ce-136">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="473ce-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="473ce-137">Recuperar la lista de Hola de tablas externas de la base de datos actual de hello:</span><span class="sxs-lookup"><span data-stu-id="473ce-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="473ce-138">toodrop tablas externas:</span><span class="sxs-lookup"><span data-stu-id="473ce-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="473ce-139">Comentarios</span><span class="sxs-lookup"><span data-stu-id="473ce-139">Remarks</span></span>
<span data-ttu-id="473ce-140">Hola datos\_cláusula de origen define el origen de datos externo de hello (un mapa de particiones) que se usa para la tabla externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="473ce-141">Hola esquema\_nombre y el objeto\_cláusulas nombre asignan Hola externo tooa tabla de definición de un esquema diferente.</span><span class="sxs-lookup"><span data-stu-id="473ce-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="473ce-142">Si se omite, se asume el esquema de hello del objeto remoto hello toobe "dbo" y su nombre se supone el nombre de tabla externa de toobe toohello idénticos que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="473ce-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="473ce-143">Esto es útil si Hola nombre de la tabla remota ya existe en la base de datos de Hola donde desea que la tabla externa de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="473ce-144">Por ejemplo, desea toodefine una tooget de tabla externa una vista agregada de las vistas de catálogo o capa de DMV en los datos de escalada horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="473ce-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="473ce-145">Puesto que las vistas de catálogo y DMV ya existen localmente, no puede utilizar sus nombres de definición de tabla externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="473ce-146">En su lugar, utilice un nombre diferente y usar la vista de catálogo de Hola u Hola nombre DMV Hola esquema\_nombre y/o objeto\_cláusulas de nombre.</span><span class="sxs-lookup"><span data-stu-id="473ce-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="473ce-147">(Vea el siguiente ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="473ce-147">(See hello example below.)</span></span> 

<span data-ttu-id="473ce-148">cláusula de distribución de Hello especifica la distribución de datos de hello utilizada para esta tabla.</span><span class="sxs-lookup"><span data-stu-id="473ce-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="473ce-149">procesador de consultas de Hello usa información de hello proporcionada Hola distribución cláusula toobuild hello más eficaces en planes de consulta.</span><span class="sxs-lookup"><span data-stu-id="473ce-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="473ce-150">**PARTICIONADA** significa datos se particionan horizontalmente a través de las bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="473ce-151">Hola clave de partición para la distribución de datos de hello es hello **< sharding_column_name >** parámetro.</span><span class="sxs-lookup"><span data-stu-id="473ce-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="473ce-152">**Replica** significa que copias idénticas de tabla Hola están presentes en cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="473ce-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="473ce-153">Es el tooensure de responsabilidad que las réplicas de hello son idénticas entre bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="473ce-154">**REDONDEAR\_ROBIN** significa que esa tabla Hola se particionan horizontalmente mediante un método de distribución depende de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="473ce-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="473ce-155">**Referencia de nivel de datos**: tabla externa de hello DDL hace referencia tooan origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="473ce-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="473ce-156">origen de datos externo de Hello especifica un mapa de particiones que proporciona la tabla externa de Hola con hello información necesarios toolocate todas las bases de datos de hello en el nivel de datos.</span><span class="sxs-lookup"><span data-stu-id="473ce-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="473ce-157">Consideraciones sobre la seguridad</span><span class="sxs-lookup"><span data-stu-id="473ce-157">Security considerations</span></span>
<span data-ttu-id="473ce-158">Los usuarios con la tabla externa de acceso toohello automáticamente acceder toohello de tabla remota subyacente en credencial de hello dada en la definición de origen de datos externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="473ce-159">Evite no deseada elevación de privilegios a través de la credencial de Hola Hola externa del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="473ce-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="473ce-160">Use GRANT o REVOKE para una tabla externa como si fuera una tabla normal.</span><span class="sxs-lookup"><span data-stu-id="473ce-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="473ce-161">Una vez que defina el origen de datos externo y las tablas externas, puede usar el T-SQL completo en las tablas externas.</span><span class="sxs-lookup"><span data-stu-id="473ce-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="473ce-162">Ejemplo: consulta de bases de datos con particiones horizontales</span><span class="sxs-lookup"><span data-stu-id="473ce-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="473ce-163">Hello siguiente consulta realiza una combinación de tres vías entre almacenes, pedidos y líneas de pedido y usa varios agregados y un filtro selectivo.</span><span class="sxs-lookup"><span data-stu-id="473ce-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="473ce-164">Se supone la partición (1) horizontal (particionamiento) y (2) que almacenes, pedidos y líneas de pedido se particionada por columna de Id. de almacenamiento de hello, y esa consulta elástico Hola puede colocar combinaciones de hello en particiones de hello y procesar parte costosa de Hola de consulta de hello en hello particiones en paralelo.</span><span class="sxs-lookup"><span data-stu-id="473ce-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="473ce-165">Procedimiento almacenado para la ejecución remota de T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="473ce-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="473ce-166">Consulta flexible también introduce un procedimiento almacenado que proporciona acceso directo toohello particiones.</span><span class="sxs-lookup"><span data-stu-id="473ce-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="473ce-167">Hola se llama al procedimiento almacenado [sp\_ejecutar \_remoto](https://msdn.microsoft.com/library/mt703714) y pueden ser utilizados tooexecute los procedimientos almacenados remotos o código de T-SQL en las bases de datos remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="473ce-168">Toma Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="473ce-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="473ce-169">Nombre de origen de datos (nvarchar): nombre de Hola Hola externa del origen de datos de tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="473ce-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="473ce-170">Consulta (nvarchar): Hola T-SQL consulta toobe ejecutado en cada partición.</span><span class="sxs-lookup"><span data-stu-id="473ce-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="473ce-171">Declaración de parámetro (nvarchar) - opcional: cadena con definiciones de tipo de datos de parámetros de hello utilizados en el parámetro de consulta de hello (por ejemplo, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="473ce-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="473ce-172">Lista de valores de los parámetros (opcional): lista separada por comas de valores de los parámetros (por ejemplo, sp_executesql)</span><span class="sxs-lookup"><span data-stu-id="473ce-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="473ce-173">Hola sp\_ejecutar\_remoto usa Hola proporcionada parámetros de invocación de Hola tooexecute Hola dada la instrucción de T-SQL en las bases de datos remoto de Hola de origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="473ce-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="473ce-174">Utiliza credenciales de Hola Hola externo origen tooconnect toohello shardmap el Administrador de datos y bases de datos remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="473ce-175">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="473ce-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="473ce-176">Conectividad para herramientas</span><span class="sxs-lookup"><span data-stu-id="473ce-176">Connectivity for tools</span></span>
<span data-ttu-id="473ce-177">Usar regular tooconnect de cadenas de conexión de SQL Server la aplicación, la inteligencia empresarial y los datos integración herramientas toohello base de datos con las definiciones de tabla externa.</span><span class="sxs-lookup"><span data-stu-id="473ce-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="473ce-178">Asegúrese de que SQL Server se admite como origen de datos para la herramienta.</span><span class="sxs-lookup"><span data-stu-id="473ce-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="473ce-179">A continuación, hacer referencia a base de datos de consulta flexible de hello como cualquier otra herramienta de toohello conectado de la base de datos de SQL Server y use tablas externas desde la herramienta o la aplicación como si fueran tablas locales.</span><span class="sxs-lookup"><span data-stu-id="473ce-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="473ce-180">Prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="473ce-180">Best practices</span></span>
* <span data-ttu-id="473ce-181">Asegúrese de que se le han otorgado esa base de datos de punto de conexión de consulta flexible de hello base de datos de access toohello shardmap y todas las particiones a través de hello que firewalls de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="473ce-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="473ce-182">Validar ni se exige la distribución de datos de hello definida por la tabla externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="473ce-183">Si la distribución de datos real es distinta del especificado en la definición de la tabla de distribución de hello, las consultas pueden producir resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="473ce-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="473ce-184">Consulta flexible actualmente no realiza eliminación de particiones cuando predicados de clave de particionamiento de Hola permitiría toosafely excluir ciertas particiones de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="473ce-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="473ce-185">Consulta flexible funciona mejor para las consultas que puede realizarse la mayor parte del cálculo de hello en particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="473ce-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="473ce-186">Normalmente se obtendrá Hola mejor rendimiento de las consultas con predicados de filtro selectivo que se pueden evaluar en particiones de Hola o combinaciones sobre Hola claves que se pueden realizar de forma alineada por partición en todas las particiones de partición.</span><span class="sxs-lookup"><span data-stu-id="473ce-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="473ce-187">Otros patrones de consulta pueden requerir grandes cantidades de datos desde el nodo principal de hello particiones toohello de tooload y pueden tener un rendimiento bajo</span><span class="sxs-lookup"><span data-stu-id="473ce-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="473ce-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="473ce-188">Next steps</span></span>

* <span data-ttu-id="473ce-189">Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="473ce-190">Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="473ce-191">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="473ce-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="473ce-192">Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="473ce-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="473ce-193">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="473ce-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
