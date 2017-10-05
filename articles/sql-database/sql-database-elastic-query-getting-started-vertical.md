---
title: "Introducción a las consultas entre bases de datos (particiones verticales) | Microsoft Docs"
description: "cómo usar la consulta de base de datos elástica con bases de datos con particiones verticales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 17158c4960e9ba9251524659c90af9aec1316774
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="c88cc-103">Introducción a las consultas entre bases de datos (particiones verticales) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="c88cc-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="c88cc-104">La consulta de base de datos elástica (vista previa) para Base de datos SQL de Azure le permite ejecutar consultas T-SQL que distribuyen varias bases de datos con un único punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="c88cc-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="c88cc-105">Este tema se aplica a [bases de datos con particiones verticales](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="c88cc-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="c88cc-106">Una vez completado, sabrá: cómo configurar y usar una Base de datos SQL de Azure para realizar consultas que distribuyan múltiples bases de datos relacionadas.</span><span class="sxs-lookup"><span data-stu-id="c88cc-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="c88cc-107">Para más información sobre la característica de consulta de bases de datos elásticas, vaya a [Información general sobre la consulta de bases de datos elásticas de Azure SQL Database](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c88cc-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c88cc-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c88cc-108">Prerequisites</span></span>

<span data-ttu-id="c88cc-109">Se debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="c88cc-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="c88cc-110">Este permiso está incluido en el permiso ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="c88cc-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="c88cc-111">Se necesitan permisos ALTER ANY EXTERNAL DATA SOURCE para hacer referencia al origen de datos subyacente.</span><span class="sxs-lookup"><span data-stu-id="c88cc-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="c88cc-112">Crear las base de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c88cc-112">Create the sample databases</span></span>
<span data-ttu-id="c88cc-113">Para empezar, debemos crear dos bases de datos, **Customers** y **Orders**, ya sea en el mismo servidor o en diferentes servidores lógicos.</span><span class="sxs-lookup"><span data-stu-id="c88cc-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="c88cc-114">Ejecute las siguientes consultas en la base de datos **Orders** para crear la tabla **OrderInformation** e introducir los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c88cc-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="c88cc-115">Ahora, ejecute la siguiente consulta en la base de datos **Customers** para crear la tabla **CustomerInformation** e introducir los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c88cc-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="c88cc-116">Creación de objetos de base de datos</span><span class="sxs-lookup"><span data-stu-id="c88cc-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="c88cc-117">Clave maestra y credenciales de ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="c88cc-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="c88cc-118">Abra SQL Server Management Studio o SQL Server Data Tools en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c88cc-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="c88cc-119">Conéctese a la base de datos Pedidos y ejecute los siguientes comandos de T-SQL:</span><span class="sxs-lookup"><span data-stu-id="c88cc-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="c88cc-120">"username" y "contraseña" deben ser el nombre de usuario y la contraseña usados para iniciar sesión en la base de datos Clientes.</span><span class="sxs-lookup"><span data-stu-id="c88cc-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="c88cc-121">Actualmente no se admite la autenticación usando Azure Active Directory con consultas elásticas.</span><span class="sxs-lookup"><span data-stu-id="c88cc-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="c88cc-122">Orígenes de datos externos</span><span class="sxs-lookup"><span data-stu-id="c88cc-122">External data sources</span></span>
<span data-ttu-id="c88cc-123">Para crear un origen de datos externo, ejecute el siguiente comando en la base de datos Pedidos:</span><span class="sxs-lookup"><span data-stu-id="c88cc-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="c88cc-124">Tablas externas</span><span class="sxs-lookup"><span data-stu-id="c88cc-124">External tables</span></span>
<span data-ttu-id="c88cc-125">Cree una tabla externa en la base de datos Pedidos, que coincida con la definición de la tabla CustomerInformation:</span><span class="sxs-lookup"><span data-stu-id="c88cc-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="c88cc-126">Ejecución de la consulta de T-SQL de la base de datos elástica de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c88cc-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="c88cc-127">Una vez que haya definido su origen de datos externo y las tablas externas, puede usar el T-SQL para consultar sus las tablas externas.</span><span class="sxs-lookup"><span data-stu-id="c88cc-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="c88cc-128">Ejecute esta consulta en la base de datos Pedidos:</span><span class="sxs-lookup"><span data-stu-id="c88cc-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="c88cc-129">Coste</span><span class="sxs-lookup"><span data-stu-id="c88cc-129">Cost</span></span>
<span data-ttu-id="c88cc-130">En la actualidad, la característica de consulta de base de datos elástica se incluye en el coste de la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="c88cc-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="c88cc-131">Para obtener información de precios, vea [Precio de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="c88cc-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c88cc-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c88cc-132">Next steps</span></span>

* <span data-ttu-id="c88cc-133">Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c88cc-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c88cc-134">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c88cc-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="c88cc-135">Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c88cc-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="c88cc-136">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c88cc-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c88cc-137">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="c88cc-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>