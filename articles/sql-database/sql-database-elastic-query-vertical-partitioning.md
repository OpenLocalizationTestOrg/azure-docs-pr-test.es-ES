---
title: Consulta entre bases de datos en la nube con diferente esquema | Microsoft Docs
description: "cómo configurar consultas entre bases de datos en particiones verticales"
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
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="c934b-103">Consulta de bases de datos elásticas para consultas entre bases de datos (particionamiento vertical)</span><span class="sxs-lookup"><span data-stu-id="c934b-103">Query across cloud databases with different schemas (preview)</span></span>
![Consultas entre tablas de bases de datos diferentes][1]

<span data-ttu-id="c934b-105">Las bases de datos con particiones verticales usan distintos conjuntos de tablas en bases de datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="c934b-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="c934b-106">Esto significa que el esquema es diferente en las distintas bases de datos.</span><span class="sxs-lookup"><span data-stu-id="c934b-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="c934b-107">Por ejemplo, todas las tablas de inventario se encuentran en una base de datos mientras que todas las relacionadas con la contabilidad se encuentran en otra.</span><span class="sxs-lookup"><span data-stu-id="c934b-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c934b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c934b-108">Prerequisites</span></span>
* <span data-ttu-id="c934b-109">El usuario debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="c934b-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="c934b-110">Este permiso está incluido en el permiso ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="c934b-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="c934b-111">Se necesitan permisos ALTER ANY EXTERNAL DATA SOURCE para hacer referencia al origen de datos subyacente.</span><span class="sxs-lookup"><span data-stu-id="c934b-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="c934b-112">Información general</span><span class="sxs-lookup"><span data-stu-id="c934b-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="c934b-113">A diferencia del particionamiento horizontal, estas instrucciones DDL no dependen de la definición de una capa de datos con un mapa de particiones mediante la biblioteca de cliente de bases de datos elásticas.</span><span class="sxs-lookup"><span data-stu-id="c934b-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="c934b-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="c934b-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="c934b-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="c934b-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="c934b-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="c934b-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="c934b-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="c934b-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="c934b-118">Creación de clave maestra y credenciales con ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="c934b-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="c934b-119">La credencial utiliza la consulta elástica para conectarse a las bases de datos remotas.</span><span class="sxs-lookup"><span data-stu-id="c934b-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="c934b-120">Asegúrese de que `<username>` no incluya ningún sufijo **"@servername"**.</span><span class="sxs-lookup"><span data-stu-id="c934b-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="c934b-121">Creación de orígenes de datos externos</span><span class="sxs-lookup"><span data-stu-id="c934b-121">Create external data sources</span></span>
<span data-ttu-id="c934b-122">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="c934b-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="c934b-123">El parámetro TYPE debe establecerse en **RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="c934b-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="c934b-124">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c934b-124">Example</span></span>
<span data-ttu-id="c934b-125">En el ejemplo siguiente se ilustra el uso de la instrucción CREATE para orígenes de datos externos.</span><span class="sxs-lookup"><span data-stu-id="c934b-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="c934b-126">Para recuperar la lista de orígenes de datos externos actuales:</span><span class="sxs-lookup"><span data-stu-id="c934b-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="c934b-127">Tablas externas</span><span class="sxs-lookup"><span data-stu-id="c934b-127">External Tables</span></span>
<span data-ttu-id="c934b-128">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="c934b-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="c934b-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c934b-129">Example</span></span>
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

<span data-ttu-id="c934b-130">En el ejemplo siguiente se muestra cómo recuperar la lista de tablas externas de la base de datos actual:</span><span class="sxs-lookup"><span data-stu-id="c934b-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="c934b-131">Comentarios</span><span class="sxs-lookup"><span data-stu-id="c934b-131">Remarks</span></span>
<span data-ttu-id="c934b-132">La consulta elástica amplía la sintaxis de la tabla externa existente para que incluya la definición de tablas externas que usan orígenes de datos externos de tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="c934b-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="c934b-133">La definición de tabla externa para el particionamiento vertical abarca los siguientes aspectos:</span><span class="sxs-lookup"><span data-stu-id="c934b-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="c934b-134">**Esquema**: el DDL de tabla externa define un esquema que las consultas pueden usar.</span><span class="sxs-lookup"><span data-stu-id="c934b-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="c934b-135">El esquema proporcionado en la definición de tabla externa debe coincidir con el de las tablas de la base de datos remota donde se almacenan los datos en sí.</span><span class="sxs-lookup"><span data-stu-id="c934b-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="c934b-136">**Referencia a base de datos remota**: el DDL de tabla externa hace referencia a un origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="c934b-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="c934b-137">El origen de datos externo especifica el nombre del servidor lógico y el nombre de la base de datos remota donde se almacenan los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="c934b-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="c934b-138">Usando un origen de datos externo como se describe en la anterior sección, la sintaxis para crear tablas externas es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c934b-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="c934b-139">La cláusula DATA_SOURCE define el origen de datos externo (es decir, la base de datos remota en el caso del particionamiento vertical) que se usa para la tabla externa.</span><span class="sxs-lookup"><span data-stu-id="c934b-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="c934b-140">Las cláusulas SCHEMA_NAME y OBJECT_NAME proporcionan la capacidad de asignar la definición de la tabla externa a una tabla en un esquema diferente de la base de datos remota, o bien a una tabla con un nombre diferente, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c934b-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="c934b-141">Esto resulta útil si desea definir una tabla externa en una vista de catálogo o DMV en la base de datos remota, o en cualquier otra situación en que el nombre de la tabla remota ya se use localmente.</span><span class="sxs-lookup"><span data-stu-id="c934b-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="c934b-142">La siguiente instrucción DDL quita una definición de tabla externa existente del catálogo local.</span><span class="sxs-lookup"><span data-stu-id="c934b-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="c934b-143">No afecta a la base de datos remota.</span><span class="sxs-lookup"><span data-stu-id="c934b-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="c934b-144">**Permisos para CREATE/DROP EXTERNAL TABLE**: se necesitan permisos ALTER ANY EXTERNAL DATA SOURCE para el DDL de tabla externa que también se necesita para hacer referencia al origen de datos subyacente.</span><span class="sxs-lookup"><span data-stu-id="c934b-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="c934b-145">Consideraciones sobre la seguridad</span><span class="sxs-lookup"><span data-stu-id="c934b-145">Security considerations</span></span>
<span data-ttu-id="c934b-146">Los usuarios con acceso a la tabla externa obtienen automáticamente acceso a las tablas remotas subyacentes con la credencial proporcionada en la definición del origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="c934b-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="c934b-147">Debe administrar con cuidado el acceso a la tabla externa para evitar la elevación de privilegios no deseada por medio de la credencial del origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="c934b-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="c934b-148">Se pueden usar permisos SQL normales para conceder o revocar el acceso a una tabla externa como si fuera una tabla normal.</span><span class="sxs-lookup"><span data-stu-id="c934b-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="c934b-149">Ejemplo: consulta de bases de datos con particiones verticales</span><span class="sxs-lookup"><span data-stu-id="c934b-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="c934b-150">La consulta siguiente realiza una combinación tridireccional entre las dos tablas locales de pedidos y líneas de pedido, y la tabla remota de clientes.</span><span class="sxs-lookup"><span data-stu-id="c934b-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="c934b-151">Es un ejemplo del caso de uso de datos de referencia para una consulta elástica:</span><span class="sxs-lookup"><span data-stu-id="c934b-151">This is an example of the reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="c934b-152">Procedimiento almacenado para la ejecución remota de T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="c934b-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="c934b-153">La consulta elástica también incluye un procedimiento almacenado que proporciona acceso directo a las particiones.</span><span class="sxs-lookup"><span data-stu-id="c934b-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="c934b-154">El procedimiento almacenado se denomina [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714) y sirve para ejecutar procedimientos almacenados remotos o código T-SQL en bases de datos remotas.</span><span class="sxs-lookup"><span data-stu-id="c934b-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="c934b-155">Toma los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="c934b-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="c934b-156">Nombre de origen de datos (nvarchar): nombre del origen de datos externo de tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="c934b-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="c934b-157">Consulta (nvarchar): la consulta T-SQL que se va a ejecutar en cada partición.</span><span class="sxs-lookup"><span data-stu-id="c934b-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="c934b-158">Declaración de parámetro (nvarchar) - opcional: cadena con definiciones de tipos de datos de los parámetros usados en el parámetro Query (como sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="c934b-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="c934b-159">Lista de valores de los parámetros (opcional): lista separada por comas de valores de los parámetros (por ejemplo, sp_executesql)</span><span class="sxs-lookup"><span data-stu-id="c934b-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="c934b-160">sp\_execute\_remote utiliza el origen de datos externo proporcionado en los parámetros de invocación para ejecutar la instrucción T-SQL determinada en las bases de datos remotas.</span><span class="sxs-lookup"><span data-stu-id="c934b-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="c934b-161">Utiliza la credencial del origen de datos externo para conectarse a la base de datos de ShardMapManager y las bases de datos remotas.</span><span class="sxs-lookup"><span data-stu-id="c934b-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="c934b-162">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c934b-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="c934b-163">Conectividad para herramientas</span><span class="sxs-lookup"><span data-stu-id="c934b-163">Connectivity for tools</span></span>
<span data-ttu-id="c934b-164">Puede usar cadenas de conexión de SQL Server normales para conectar sus herramientas de integración de datos y de BI con bases de datos en el servidor de base de datos SQL en que se habilitó la consulta elástica y se definieron las tablas externas.</span><span class="sxs-lookup"><span data-stu-id="c934b-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="c934b-165">Asegúrese de que SQL Server se admite como origen de datos para la herramienta.</span><span class="sxs-lookup"><span data-stu-id="c934b-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="c934b-166">Después, consulte la base de datos de consulta elástica y sus tablas externas como cualquier otra base de datos de SQL Server a la que se conectaría con su herramienta.</span><span class="sxs-lookup"><span data-stu-id="c934b-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="c934b-167">Prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="c934b-167">Best practices</span></span>
* <span data-ttu-id="c934b-168">Asegúrese de que se conceda a la base de datos de punto de conexión de consulta elástica acceso a la base de datos remota habilitando el acceso a los Servicios de Azure en su configuración de firewall de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c934b-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="c934b-169">Compruebe también que la credencial proporcionada en la definición del origen de datos externo pueda iniciar sesión correctamente en la base de datos remota y tenga los permisos para acceder a la tabla remota.</span><span class="sxs-lookup"><span data-stu-id="c934b-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="c934b-170">Una consulta elástica funciona mejor para aquellas consultas en que la mayor parte del cálculo se puede realizar en las bases de datos remotas.</span><span class="sxs-lookup"><span data-stu-id="c934b-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="c934b-171">Normalmente, el máximo rendimiento de las consultas se obtiene con predicados de filtro selectivos que se pueden evaluar en las bases de datos remotas o combinaciones que se pueden realizar totalmente en la base de datos remota.</span><span class="sxs-lookup"><span data-stu-id="c934b-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="c934b-172">Es posible que otros patrones de consulta necesiten cargar grandes cantidades de datos desde la base de datos remota y pueden experimentar un rendimiento deficiente.</span><span class="sxs-lookup"><span data-stu-id="c934b-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c934b-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c934b-173">Next steps</span></span>

* <span data-ttu-id="c934b-174">Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c934b-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c934b-175">Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales) (versión preliminar)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="c934b-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="c934b-176">Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c934b-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="c934b-177">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c934b-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c934b-178">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="c934b-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
