---
title: "Informes de bases de datos escaladas horizontalmente en la nube (partición horizontal) | Microsoft Docs"
description: "cómo utilizar consultas de bases de datos cruzadas"
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
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="e1c88-103">Informes de bases de datos escaladas horizontalmente en la nube (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="e1c88-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="e1c88-104">Puede crear informes de varias bases de datos SQL de Azure desde un único punto de conexión mediante una [consulta elástica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1c88-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="e1c88-105">Las bases de datos deben tener particiones horizontales (también conocidas como "particiones").</span><span class="sxs-lookup"><span data-stu-id="e1c88-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="e1c88-106">Si tiene una base de datos, consulte [Conversión de bases de datos existentes para usar herramientas para bases de datos elásticas](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="e1c88-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="e1c88-107">Para comprender los objetos SQL necesarios para realizar consultas, consulte [Informes de bases de datos escaladas horizontalmente en la nube (versión preliminar)](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="e1c88-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1c88-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e1c88-108">Prerequisites</span></span>
<span data-ttu-id="e1c88-109">Descargue [Introducción al ejemplo de herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e1c88-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="e1c88-110">Creación de un administrador de mapas de particiones con la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1c88-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="e1c88-111">Aquí se creará un administrador de mapas de particiones junto con varias particiones, seguido de la inserción de datos en las particiones.</span><span class="sxs-lookup"><span data-stu-id="e1c88-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="e1c88-112">Si resulta que ya dispone de la configuración de particiones con almacenes de datos en ellas, puede omitir los pasos siguientes y pasar a la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="e1c88-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="e1c88-113">Cree y ejecute la aplicación de ejemplo **Introducción a las herramientas de base de datos elástica** .</span><span class="sxs-lookup"><span data-stu-id="e1c88-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="e1c88-114">Siga los pasos hasta el paso 7 de la sección [Descarga y ejecución de la aplicación de ejemplo](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="e1c88-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="e1c88-115">Al final del paso 7, verá la siguiente línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="e1c88-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![símbolo del sistema][1]
2. <span data-ttu-id="e1c88-117">En la ventana de comandos, escriba "1" y pulse **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="e1c88-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="e1c88-118">De esta forma, se creará el administrador de mapas de particiones y se agregarán dos particiones al servidor.</span><span class="sxs-lookup"><span data-stu-id="e1c88-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="e1c88-119">A continuación, escriba "3" y pulse **Entrar**; repita la acción cuatro veces.</span><span class="sxs-lookup"><span data-stu-id="e1c88-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="e1c88-120">De esta forma, se insertan las filas de datos de ejemplo en sus particiones.</span><span class="sxs-lookup"><span data-stu-id="e1c88-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="e1c88-121">[Azure Portal](https://portal.azure.com) debería mostrar tres nuevas bases de datos en el servidor:</span><span class="sxs-lookup"><span data-stu-id="e1c88-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Confirmación de Visual Studio][2]

   <span data-ttu-id="e1c88-123">En este momento, se admiten las consultas entre bases de datos a través de las bibliotecas de cliente de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="e1c88-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="e1c88-124">Por ejemplo, use la opción 4 en la ventana de comandos.</span><span class="sxs-lookup"><span data-stu-id="e1c88-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="e1c88-125">Los resultados de una consulta de varias particiones son siempre una **UNIÓN DE TODOS** los resultados de todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="e1c88-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="e1c88-126">En la siguiente sección, crearemos un extremo de la base de datos de ejemplo que admite las consultas más completas de los datos entre las particiones.</span><span class="sxs-lookup"><span data-stu-id="e1c88-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="e1c88-127">Creación una base de datos de consulta elástica</span><span class="sxs-lookup"><span data-stu-id="e1c88-127">Create an elastic query database</span></span>
1. <span data-ttu-id="e1c88-128">Abra [Azure Portal](https://portal.azure.com) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="e1c88-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="e1c88-129">Cree una nueva Base de datos SQL de Azure en el mismo servidor que la configuración de la partición.</span><span class="sxs-lookup"><span data-stu-id="e1c88-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="e1c88-130">Utilice el nombre "ElasticDBQuery" para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="e1c88-130">Name the database "ElasticDBQuery."</span></span>

    ![Portal de Azure y nivel de precios][3]

    > [!NOTE]
    > <span data-ttu-id="e1c88-132">puede usar una base de datos existente.</span><span class="sxs-lookup"><span data-stu-id="e1c88-132">you can use an existing database.</span></span> <span data-ttu-id="e1c88-133">Si puede hacerlo, no debe ser una de las particiones en las que desee ejecutar las consultas.</span><span class="sxs-lookup"><span data-stu-id="e1c88-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="e1c88-134">Esta base de datos se usará para crear los objetos de metadatos para una consulta de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="e1c88-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="e1c88-135">Creación de objetos de base de datos</span><span class="sxs-lookup"><span data-stu-id="e1c88-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="e1c88-136">Clave maestra y credenciales de ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="e1c88-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="e1c88-137">Se usan para conectarse al administrador de mapas de particiones y particiones:</span><span class="sxs-lookup"><span data-stu-id="e1c88-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="e1c88-138">Abra SQL Server Management Studio o SQL Server Data Tools en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1c88-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="e1c88-139">Conéctese a la base de datos ElasticDBQuery y ejecute los siguientes comandos de T-SQL:</span><span class="sxs-lookup"><span data-stu-id="e1c88-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="e1c88-140">El nombre de usuario y la contraseña deben coincidir con la información de inicio de sesión del paso 6 de [Descarga y ejecución de la aplicación de ejemplo](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) en [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e1c88-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="e1c88-141">Orígenes de datos externos</span><span class="sxs-lookup"><span data-stu-id="e1c88-141">External data sources</span></span>
<span data-ttu-id="e1c88-142">Para crear un origen de datos externo, ejecute el siguiente comando en la base de datos ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="e1c88-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="e1c88-143">"CustomerIDShardMap" es el nombre del mapa de particiones, si ha creado el administrador de mapa de particiones y el mapa de particiones con el ejemplo de herramientas de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="e1c88-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="e1c88-144">Sin embargo, si usó la configuración personalizada para este ejemplo, debe ser el nombre de mapa de particiones que eligió en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c88-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="e1c88-145">Tablas externas</span><span class="sxs-lookup"><span data-stu-id="e1c88-145">External tables</span></span>
<span data-ttu-id="e1c88-146">Cree una tabla externa que coincida con la tabla Clientes en las particiones ejecutando el siguiente comando en la base de datos ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="e1c88-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="e1c88-147">Ejecución de la consulta de T-SQL de la base de datos elástica de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1c88-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="e1c88-148">Una vez que haya definido el origen de datos externo y las tablas externas, puede usar el T-SQL completo en las tablas externas.</span><span class="sxs-lookup"><span data-stu-id="e1c88-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="e1c88-149">Ejecute esta consulta en la base de datos ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="e1c88-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="e1c88-150">Observará que la consulta agrega resultados de todas las particiones y proporciona el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="e1c88-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![Detalles de salida][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="e1c88-152">Importación de los resultados de la consulta de base de datos elástica a Excel</span><span class="sxs-lookup"><span data-stu-id="e1c88-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="e1c88-153">Puede importar los resultados de una consulta a un archivo Excel.</span><span class="sxs-lookup"><span data-stu-id="e1c88-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="e1c88-154">Inicie Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="e1c88-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="e1c88-155">Diríjase a la barra de herramientas **Datos** .</span><span class="sxs-lookup"><span data-stu-id="e1c88-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="e1c88-156">Haga clic en **Desde otros orígenes** y luego en **Desde SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e1c88-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importación de Excel desde otros orígenes][5]
4. <span data-ttu-id="e1c88-158">En el **Asistente de conexión de datos** , escriba el nombre del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e1c88-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="e1c88-159">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e1c88-159">Then click **Next**.</span></span>
5. <span data-ttu-id="e1c88-160">En el cuadro de diálogo **Seleccione la base de datos que contiene la información que desea**, seleccione la base de datos **ElasticDBQuery**.</span><span class="sxs-lookup"><span data-stu-id="e1c88-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="e1c88-161">Seleccione la tabla **Customers** de la vista de lista y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e1c88-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="e1c88-162">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="e1c88-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="e1c88-163">En el formulario **Importar datos**, en **Seleccione cómo desea ver estos datos en el libro**, seleccione **Tabla** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e1c88-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="e1c88-164">Todas las filas de la tabla **Clientes** , almacenadas en distintas particiones, completan la hoja de Excel.</span><span class="sxs-lookup"><span data-stu-id="e1c88-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="e1c88-165">Ahora puede usar las funciones de visualización de datos decisivas de Excel.</span><span class="sxs-lookup"><span data-stu-id="e1c88-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="e1c88-166">Puede usar la cadena de conexión con el nombre de servidor, el nombre de base de datos y las credenciales para conectar su BI y las herramientas de integración de datos a la base de datos de consulta elástica.</span><span class="sxs-lookup"><span data-stu-id="e1c88-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="e1c88-167">Asegúrese de que SQL Server se admite como origen de datos para la herramienta.</span><span class="sxs-lookup"><span data-stu-id="e1c88-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="e1c88-168">Puede consultar la base de datos de consulta elástica y las tablas externas como cualquier otra base de datos SQL Server y las tablas de SQL Server que quiera conectar con la herramienta.</span><span class="sxs-lookup"><span data-stu-id="e1c88-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="e1c88-169">Coste</span><span class="sxs-lookup"><span data-stu-id="e1c88-169">Cost</span></span>
<span data-ttu-id="e1c88-170">No hay ningún cargo adicional por usar la característica de consulta de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="e1c88-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="e1c88-171">Para obtener información sobre los precios, consulte [Detalles de precios de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="e1c88-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1c88-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1c88-172">Next steps</span></span>

* <span data-ttu-id="e1c88-173">Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1c88-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="e1c88-174">Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="e1c88-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="e1c88-175">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="e1c88-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="e1c88-176">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="e1c88-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="e1c88-177">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="e1c88-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
