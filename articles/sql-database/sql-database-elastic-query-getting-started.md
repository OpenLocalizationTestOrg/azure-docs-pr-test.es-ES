---
title: "aaaReport entre bases de datos de escala horizontal en la nube (creación de particiones horizontales) | Documentos de Microsoft"
description: "¿Cómo toouse entre las consultas de base de datos de base de datos"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="c6855-103">Informes de bases de datos escaladas horizontalmente en la nube (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="c6855-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="c6855-104">Puede crear informes de varias bases de datos SQL de Azure desde un único punto de conexión mediante una [consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6855-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="c6855-105">las bases de datos de Hello deben crear particiones horizontalmente (también conocida como "particionadas").</span><span class="sxs-lookup"><span data-stu-id="c6855-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="c6855-106">Si tiene una base de datos existente, vea [existente migrar bases de datos de las bases de datos fuera de tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="c6855-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="c6855-107">los objetos SQL de hello toounderstand necesarios tooquery, consulte [consulta entre bases de datos con particiones horizontales](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="c6855-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6855-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6855-108">Prerequisites</span></span>
<span data-ttu-id="c6855-109">Descargue y ejecute hello [cómo empezar a usar el ejemplo de herramientas de la base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6855-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="c6855-110">Crear un mapa de particiones administrador mediante la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="c6855-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="c6855-111">A continuación creará un mapa de particiones administrador junto con varias particiones, seguido por la inserción de datos en particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6855-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="c6855-112">Si se encontrara tooalready tienen el programa de instalación de particiones con datos particionados en ellos, puede omitir Hola pasos y mover toohello siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="c6855-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="c6855-113">Compile y ejecute hello **Introducción a las herramientas de base de datos elástica** aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c6855-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="c6855-114">Siga los pasos de hello hasta el paso 7 de la sección de hello [descargue y ejecute la aplicación de ejemplo de Hola](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="c6855-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="c6855-115">Al final de saludo del paso 7, verá Hola después de símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="c6855-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![símbolo del sistema][1]
2. <span data-ttu-id="c6855-117">En la ventana de comandos de hello, escriba "1" y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="c6855-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="c6855-118">Esto crea el Administrador de mapa de particiones de Hola y agrega dos particiones toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="c6855-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="c6855-119">A continuación, escriba "3" y presione **ENTRAR**; repita la acción de hello cuatro veces.</span><span class="sxs-lookup"><span data-stu-id="c6855-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="c6855-120">De esta forma, se insertan las filas de datos de ejemplo en sus particiones.</span><span class="sxs-lookup"><span data-stu-id="c6855-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="c6855-121">Hola [portal de Azure](https://portal.azure.com) debe mostrar tres nuevas bases de datos en el servidor:</span><span class="sxs-lookup"><span data-stu-id="c6855-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Confirmación de Visual Studio][2]

   <span data-ttu-id="c6855-123">En este momento, se admiten las consultas entre bases de datos a través de bibliotecas de cliente de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="c6855-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="c6855-124">Por ejemplo, utilice la opción 4 en la ventana de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6855-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="c6855-125">Hola resultados de una consulta de varias particiones siempre son un **UNION ALL** resultados de Hola de todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="c6855-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="c6855-126">En la siguiente sección hello, creamos un punto de conexión de base de datos de ejemplo que admite las consultas más completa de los datos de hello entre las particiones.</span><span class="sxs-lookup"><span data-stu-id="c6855-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="c6855-127">Creación una base de datos de consulta elástica</span><span class="sxs-lookup"><span data-stu-id="c6855-127">Create an elastic query database</span></span>
1. <span data-ttu-id="c6855-128">Abra hello [portal de Azure](https://portal.azure.com) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="c6855-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="c6855-129">Crear una nueva base de datos de SQL Azure en hello mismo servidor que el programa de instalación de la partición.</span><span class="sxs-lookup"><span data-stu-id="c6855-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="c6855-130">Base de datos de nombres Hola "ElasticDBQuery."</span><span class="sxs-lookup"><span data-stu-id="c6855-130">Name hello database "ElasticDBQuery."</span></span>

    ![Portal de Azure y nivel de precios][3]

    > [!NOTE]
    > <span data-ttu-id="c6855-132">puede usar una base de datos existente.</span><span class="sxs-lookup"><span data-stu-id="c6855-132">you can use an existing database.</span></span> <span data-ttu-id="c6855-133">Si puede hacerlo, no debe ser una de las particiones de Hola que desearía tooexecute las consultas en.</span><span class="sxs-lookup"><span data-stu-id="c6855-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="c6855-134">Esta base de datos se usará para crear objetos de metadatos para una consulta de base de datos elástica de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6855-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="c6855-135">Creación de objetos de base de datos</span><span class="sxs-lookup"><span data-stu-id="c6855-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="c6855-136">Clave maestra y credenciales de ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="c6855-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="c6855-137">Se trata de administrador de asignación de tooconnect usado toohello particiones y las particiones de hello:</span><span class="sxs-lookup"><span data-stu-id="c6855-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="c6855-138">Abra SQL Server Management Studio o SQL Server Data Tools en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6855-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="c6855-139">Conectar la base de datos de tooElasticDBQuery y ejecute hello siga los comandos del código T-SQL:</span><span class="sxs-lookup"><span data-stu-id="c6855-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="c6855-140">"username" y "password" debe ser Hola igual como información de inicio de sesión utilizada en el paso 6 de [descargue y ejecute la aplicación de ejemplo de Hola](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) en [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6855-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="c6855-141">Orígenes de datos externos</span><span class="sxs-lookup"><span data-stu-id="c6855-141">External data sources</span></span>
<span data-ttu-id="c6855-142">toocreate un origen de datos externo, ejecute hello siguiente comando en la base de datos de Hola ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="c6855-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="c6855-143">"CustomerIDShardMap" es el nombre de hello del mapa de particiones de hello, si creó mapa de particiones de Hola y mapa de particiones con el ejemplo de herramientas de base de datos elástica Hola el administrador.</span><span class="sxs-lookup"><span data-stu-id="c6855-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="c6855-144">Sin embargo, si utiliza la configuración personalizada de este ejemplo, a continuación, debe ser nombre de asignación de particiones de Hola que eligió en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6855-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="c6855-145">Tablas externas</span><span class="sxs-lookup"><span data-stu-id="c6855-145">External tables</span></span>
<span data-ttu-id="c6855-146">Crear una tabla externa que coincide con la tabla de clientes de hello en particiones de hello ejecutando el siguiente comando en la base de datos de ElasticDBQuery de hello:</span><span class="sxs-lookup"><span data-stu-id="c6855-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="c6855-147">Ejecución de la consulta de T-SQL de la base de datos elástica de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6855-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="c6855-148">Una vez que haya definido el origen de datos externo y las tablas externas, puede usar el T-SQL completo en las tablas externas.</span><span class="sxs-lookup"><span data-stu-id="c6855-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="c6855-149">Ejecute esta consulta en la base de datos de Hola ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="c6855-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="c6855-150">Observará que consultan hello agrega los resultados de todas las particiones de Hola y proporciona Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="c6855-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Detalles de salida][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="c6855-152">Importar tooExcel de resultados de consulta de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="c6855-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="c6855-153">Puede importar los resultados de Hola desde un consulta tooan del archivo de Excel.</span><span class="sxs-lookup"><span data-stu-id="c6855-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="c6855-154">Inicie Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="c6855-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="c6855-155">Navegue toohello **datos** la cinta de opciones.</span><span class="sxs-lookup"><span data-stu-id="c6855-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="c6855-156">Haga clic en **Desde otros orígenes** y luego en **Desde SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c6855-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importación de Excel desde otros orígenes][5]
4. <span data-ttu-id="c6855-158">Hola **Asistente para la conexión de datos** escriba credenciales de inicio de sesión y nombre de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6855-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="c6855-159">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6855-159">Then click **Next**.</span></span>
5. <span data-ttu-id="c6855-160">En el cuadro de diálogo de hello **base de datos de hello Select que contiene datos de Hola que desee**, seleccione hello **ElasticDBQuery** base de datos.</span><span class="sxs-lookup"><span data-stu-id="c6855-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="c6855-161">Seleccione hello **clientes** de tabla en la vista de lista de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6855-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="c6855-162">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c6855-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="c6855-163">Hola **importar datos** formulario, en **Seleccione cómo desea que tooview estos datos en el libro**, seleccione **tabla** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c6855-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="c6855-164">Todas las filas de Hola **clientes** tabla, almacenado en particiones diferentes rellenar la hoja de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6855-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="c6855-165">Ahora puede usar las funciones de visualización de datos decisivas de Excel.</span><span class="sxs-lookup"><span data-stu-id="c6855-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="c6855-166">Puede usar la cadena de conexión de hello con el nombre del servidor, nombre de base de datos y las credenciales tooconnect su BI y datos integración herramientas toohello elástico consultar base de datos.</span><span class="sxs-lookup"><span data-stu-id="c6855-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="c6855-167">Asegúrese de que SQL Server se admite como origen de datos para la herramienta.</span><span class="sxs-lookup"><span data-stu-id="c6855-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="c6855-168">Puede hacer referencia a base de datos de consulta flexible de toohello y tablas externas al igual que cualquier otra base de datos de SQL Server y las tablas de SQL Server que se conectará toowith la herramienta.</span><span class="sxs-lookup"><span data-stu-id="c6855-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="c6855-169">Coste</span><span class="sxs-lookup"><span data-stu-id="c6855-169">Cost</span></span>
<span data-ttu-id="c6855-170">No hay ningún cargo adicional para usar la característica de consulta de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="c6855-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="c6855-171">Para obtener información sobre los precios, consulte [Detalles de precios de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="c6855-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6855-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6855-172">Next steps</span></span>

* <span data-ttu-id="c6855-173">Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6855-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c6855-174">Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="c6855-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="c6855-175">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c6855-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="c6855-176">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c6855-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c6855-177">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="c6855-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
