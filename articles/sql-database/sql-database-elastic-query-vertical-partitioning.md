---
title: "las bases de datos aaaQuery a través de la nube con esquemas diferentes | Documentos de Microsoft"
description: "¿Cómo tooset consultas entre bases de datos en particiones verticales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="95015-103">Consulta de bases de datos elásticas para consultas entre bases de datos (particionamiento vertical)</span><span class="sxs-lookup"><span data-stu-id="95015-103">Query across cloud databases with different schemas (preview)</span></span>
![Consultas entre tablas de bases de datos diferentes][1]

<span data-ttu-id="95015-105">Las bases de datos con particiones verticales usan distintos conjuntos de tablas en bases de datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="95015-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="95015-106">Esto significa que el esquema hello es diferente en distintas bases de datos.</span><span class="sxs-lookup"><span data-stu-id="95015-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="95015-107">Por ejemplo, todas las tablas de inventario se encuentran en una base de datos mientras que todas las relacionadas con la contabilidad se encuentran en otra.</span><span class="sxs-lookup"><span data-stu-id="95015-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="95015-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="95015-108">Prerequisites</span></span>
* <span data-ttu-id="95015-109">usuario de Hello debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="95015-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="95015-110">Este permiso se incluye con el permiso ALTER DATABASE Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="95015-111">Los permisos ALTER ANY EXTERNAL DATA SOURCE son toohello toorefer necesario el origen de datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="95015-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="95015-112">Información general</span><span class="sxs-lookup"><span data-stu-id="95015-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="95015-113">A diferencia de con particiones horizontales, estas instrucciones de DDL no dependen de definir una capa de datos con un mapa de particiones a través de la biblioteca de cliente de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="95015-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="95015-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="95015-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="95015-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="95015-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="95015-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="95015-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="95015-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="95015-118">Creación de clave maestra y credenciales con ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="95015-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="95015-119">se utiliza la credencial de Hola Hola consulta elástico tooconnect tooyour remoto las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="95015-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="95015-120">Asegúrese de que hello `<username>` no incluye ningún **"@servername"** sufijo.</span><span class="sxs-lookup"><span data-stu-id="95015-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="95015-121">Creación de orígenes de datos externos</span><span class="sxs-lookup"><span data-stu-id="95015-121">Create external data sources</span></span>
<span data-ttu-id="95015-122">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="95015-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="95015-123">debe establecer el parámetro de tipo Hello demasiado**RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="95015-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="95015-124">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="95015-124">Example</span></span>
<span data-ttu-id="95015-125">Hello en el ejemplo siguiente se muestra hello uso de hello instrucción CREATE para orígenes de datos externos.</span><span class="sxs-lookup"><span data-stu-id="95015-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="95015-126">lista de hello tooretrieve actual orígenes de datos externos:</span><span class="sxs-lookup"><span data-stu-id="95015-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="95015-127">Tablas externas</span><span class="sxs-lookup"><span data-stu-id="95015-127">External Tables</span></span>
<span data-ttu-id="95015-128">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="95015-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="95015-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="95015-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="95015-130">Hola de ejemplo siguiente muestra cómo tooretrieve Hola lista de tablas externas de la base de datos actual de hello:</span><span class="sxs-lookup"><span data-stu-id="95015-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="95015-131">Comentarios</span><span class="sxs-lookup"><span data-stu-id="95015-131">Remarks</span></span>
<span data-ttu-id="95015-132">Consulta flexible extiende Hola existente tabla externa sintaxis toodefine tablas externas que utilizan orígenes de datos externos del tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="95015-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="95015-133">Una definición de tabla externa para el particionamiento vertical trata Hola siguientes aspectos:</span><span class="sxs-lookup"><span data-stu-id="95015-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="95015-134">**Esquema**: tabla externa de hello DDL define un esquema que pueden usar las consultas.</span><span class="sxs-lookup"><span data-stu-id="95015-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="95015-135">esquema de Hello proporcionado en la definición de tabla externa debe toomatch esquema de Hola de tablas de hello en hello bases de datos remoto donde se almacenan los datos reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="95015-136">**Referencia de base de datos remota**: tabla externa de hello DDL hace referencia tooan origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="95015-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="95015-137">origen de datos externo de Hello especifica el nombre del servidor lógico de Hola y el nombre de base de datos de hello bases de datos remoto donde se almacenan datos de tabla real de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="95015-138">Usa un origen de datos externos como se describe en la sección anterior de hello, tablas externas de hello sintaxis toocreate es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="95015-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="95015-139">cláusula de Hello DATA_SOURCE define el origen de datos externo de hello (es decir, Hola base de datos remota en el caso de las particiones verticales) que se usa para la tabla externa de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="95015-140">cláusulas de Hello SCHEMA_NAME y OBJECT_NAME proporcionan Hola capacidad toomap Hola externo tooa tabla de definición de un esquema diferente en base de datos remota de Hola o tabla tooa con un nombre distinto, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="95015-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="95015-141">Esto es útil si desea que toodefine una vista de catálogo de tabla externa tooa o DMV en la base de datos remota - o cualquier otra situación donde nombre de la tabla remota de hello ya está en uso localmente.</span><span class="sxs-lookup"><span data-stu-id="95015-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="95015-142">Hello siguiente instrucción DDL quita una definición de tabla externa existente de catálogo local Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="95015-143">No afecta a la base de datos remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="95015-144">**Permisos para la tabla externa de CREATE/DROP**: se necesitan permisos ALTER ANY EXTERNAL DATA SOURCE de tabla externa DDL que también es necesario toorefer toohello origen de datos subyacente.</span><span class="sxs-lookup"><span data-stu-id="95015-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="95015-145">Consideraciones sobre la seguridad</span><span class="sxs-lookup"><span data-stu-id="95015-145">Security considerations</span></span>
<span data-ttu-id="95015-146">Los usuarios con la tabla externa de acceso toohello automáticamente acceder toohello de tabla remota subyacente en credencial de hello dada en la definición de origen de datos externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="95015-147">Debe administrar con cuidado tabla externa de acceso toohello elevación de tooavoid no deseada de orden de privilegios a través de la credencial de Hola Hola externa del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="95015-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="95015-148">Permisos normales de SQL pueden ser usado tooGRANT o tabla externa de REVOCAR acceso tooan solo como si fuera una tabla normal.</span><span class="sxs-lookup"><span data-stu-id="95015-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="95015-149">Ejemplo: consulta de bases de datos con particiones verticales</span><span class="sxs-lookup"><span data-stu-id="95015-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="95015-150">Hello siguiente consulta realiza una combinación de tres vías entre dos tablas locales Hola para pedidos y líneas de pedido y tabla remota de Hola para los clientes.</span><span class="sxs-lookup"><span data-stu-id="95015-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="95015-151">Este es un ejemplo de Hola caso de uso de datos de referencia de consulta flexible:</span><span class="sxs-lookup"><span data-stu-id="95015-151">This is an example of hello reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="95015-152">Procedimiento almacenado para la ejecución remota de T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="95015-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="95015-153">Consulta flexible también introduce un procedimiento almacenado que proporciona acceso directo toohello particiones.</span><span class="sxs-lookup"><span data-stu-id="95015-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="95015-154">Hola se llama al procedimiento almacenado [sp\_ejecutar \_remoto](https://msdn.microsoft.com/library/mt703714) y pueden ser utilizados tooexecute los procedimientos almacenados remotos o código de T-SQL en las bases de datos remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="95015-155">Toma Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="95015-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="95015-156">Nombre de origen de datos (nvarchar): nombre de Hola Hola externa del origen de datos de tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="95015-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="95015-157">Consulta (nvarchar): Hola T-SQL consulta toobe ejecutado en cada partición.</span><span class="sxs-lookup"><span data-stu-id="95015-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="95015-158">Declaración de parámetro (nvarchar) - opcional: cadena con definiciones de tipo de datos de parámetros de hello utilizados en el parámetro de consulta de hello (por ejemplo, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="95015-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="95015-159">Lista de valores de los parámetros (opcional): lista separada por comas de valores de los parámetros (por ejemplo, sp_executesql)</span><span class="sxs-lookup"><span data-stu-id="95015-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="95015-160">Hola sp\_ejecutar\_remoto usa Hola proporcionada parámetros de invocación de Hola tooexecute Hola dada la instrucción de T-SQL en las bases de datos remoto de Hola de origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="95015-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="95015-161">Utiliza credenciales de Hola Hola externo origen tooconnect toohello shardmap el Administrador de datos y bases de datos remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="95015-162">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="95015-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="95015-163">Conectividad para herramientas</span><span class="sxs-lookup"><span data-stu-id="95015-163">Connectivity for tools</span></span>
<span data-ttu-id="95015-164">Puede usar el toodatabases de herramientas de integración de BI y los datos de regular tooconnect de cadenas de conexión de SQL Server en servidor de base de datos SQL de hello cuya consulta elástico habilitado y tablas externas definidas.</span><span class="sxs-lookup"><span data-stu-id="95015-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="95015-165">Asegúrese de que SQL Server se admite como origen de datos para la herramienta.</span><span class="sxs-lookup"><span data-stu-id="95015-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="95015-166">A continuación, consulte toohello consultar elástico base de datos y sus tablas externas al igual que cualquier base datos de SQL Server que se conectará toowith la herramienta.</span><span class="sxs-lookup"><span data-stu-id="95015-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="95015-167">Prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="95015-167">Best practices</span></span>
* <span data-ttu-id="95015-168">Asegúrese de que esa base de datos de punto de conexión de consulta flexible de Hola se le han otorgado base de datos de access toohello remoto al habilitar el acceso para los servicios de Azure en su configuración de firewall de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="95015-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="95015-169">Asegúrese también de esa credencial Hola siempre que en datos externos de hello definición de origen puede iniciar sesión correctamente en la base de datos remota de Hola y tiene la tabla remota de hello permisos tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="95015-170">Consulta flexible funciona mejor para las consultas donde es posible la mayor parte del cálculo de hello en bases de datos remotas de Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="95015-171">Se obtiene normalmente Hola mejor rendimiento de las consultas con predicados de filtro selectivo que se pueden evaluar en bases de datos remotas de Hola o combinaciones que se pueden realizar por completo en la base de datos remota Hola.</span><span class="sxs-lookup"><span data-stu-id="95015-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="95015-172">Otros patrones de consulta pueden requerir grandes cantidades de datos de la base de datos remota Hola de tooload y pueden tener un rendimiento bajo.</span><span class="sxs-lookup"><span data-stu-id="95015-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="95015-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95015-173">Next steps</span></span>

* <span data-ttu-id="95015-174">Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95015-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="95015-175">Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales) (versión preliminar)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="95015-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="95015-176">Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="95015-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="95015-177">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="95015-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="95015-178">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="95015-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
