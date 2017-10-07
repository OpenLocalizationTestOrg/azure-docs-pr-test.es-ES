---
title: "aaaGet a trabajar con consultas entre bases de datos (creación de particiones verticales) | Documentos de Microsoft"
description: "la consulta de base de datos elástica toouse con dividido verticalmente las bases de datos"
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
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="83444-103">Introducción a las consultas entre bases de datos (particiones verticales) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="83444-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="83444-104">Consulta de base de datos elástica (versión preliminar) para la base de datos de SQL Azure le permite toorun consultas de T-SQL que abarcan varias bases de datos con un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="83444-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="83444-105">En este tema se aplica demasiado[dividido verticalmente las bases de datos](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="83444-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="83444-106">Cuando haya completado, tendrá que: Obtenga información acerca de cómo tooconfigure y usar una base de datos de SQL Azure tooperform las consultas que usan varias bases de datos relacionadas.</span><span class="sxs-lookup"><span data-stu-id="83444-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="83444-107">Para obtener más información acerca de la característica de consulta de base de datos elástica hello, visite [información general sobre la consulta de base de datos elástica de base de datos de SQL Azure](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83444-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83444-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="83444-108">Prerequisites</span></span>

<span data-ttu-id="83444-109">Se debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="83444-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="83444-110">Este permiso se incluye con el permiso ALTER DATABASE Hola.</span><span class="sxs-lookup"><span data-stu-id="83444-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="83444-111">Los permisos ALTER ANY EXTERNAL DATA SOURCE son toohello toorefer necesario el origen de datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="83444-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="83444-112">Crear bases de datos de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="83444-112">Create hello sample databases</span></span>
<span data-ttu-id="83444-113">toostart con, necesitamos toocreate dos bases de datos, **clientes** y **pedidos**, ya sea en Hola iguales o distintos servidores lógicos.</span><span class="sxs-lookup"><span data-stu-id="83444-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="83444-114">Ejecute hello las siguientes consultas en hello **pedidos** Hola de base de datos toocreate **Informacióndepedido** tabla y entrada de datos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="83444-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="83444-115">Ahora, ejecute la consulta en hello siguiente **clientes** Hola de base de datos toocreate **Informacióndecliente** tabla y entrada de datos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="83444-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="83444-116">Creación de objetos de base de datos</span><span class="sxs-lookup"><span data-stu-id="83444-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="83444-117">Clave maestra y credenciales de ámbito de base de datos</span><span class="sxs-lookup"><span data-stu-id="83444-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="83444-118">Abra SQL Server Management Studio o SQL Server Data Tools en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83444-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="83444-119">Conectar la base de datos de pedidos de toohello y ejecute hello siga los comandos del código T-SQL:</span><span class="sxs-lookup"><span data-stu-id="83444-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="83444-120">Hola "username" y "password" deben ser el nombre de usuario de Hola y contraseña utilizados toologin en base de datos de los clientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="83444-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="83444-121">Actualmente no se admite la autenticación usando Azure Active Directory con consultas elásticas.</span><span class="sxs-lookup"><span data-stu-id="83444-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="83444-122">Orígenes de datos externos</span><span class="sxs-lookup"><span data-stu-id="83444-122">External data sources</span></span>
<span data-ttu-id="83444-123">toocreate un origen de datos externo, ejecute hello siguiente comando en la base de datos de pedidos de hello:</span><span class="sxs-lookup"><span data-stu-id="83444-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="83444-124">Tablas externas</span><span class="sxs-lookup"><span data-stu-id="83444-124">External tables</span></span>
<span data-ttu-id="83444-125">Crear una tabla externa en hello pedidos base de datos que coincide con la definición de Hola de tabla de hello Informacióndecliente:</span><span class="sxs-lookup"><span data-stu-id="83444-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="83444-126">Ejecución de la consulta de T-SQL de la base de datos elástica de ejemplo</span><span class="sxs-lookup"><span data-stu-id="83444-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="83444-127">Una vez que haya definido el origen de datos externo y las tablas externas ahora puede usar las tablas externas tooquery de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="83444-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="83444-128">Ejecute esta consulta en la base de datos de pedidos de hello:</span><span class="sxs-lookup"><span data-stu-id="83444-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="83444-129">Coste</span><span class="sxs-lookup"><span data-stu-id="83444-129">Cost</span></span>
<span data-ttu-id="83444-130">Actualmente, característica de consulta de base de datos elástica Hola se incluye en el costo de saludo de la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="83444-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="83444-131">Para obtener información de precios, vea [Precio de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="83444-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="83444-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="83444-132">Next steps</span></span>

* <span data-ttu-id="83444-133">Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83444-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="83444-134">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="83444-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="83444-135">Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="83444-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="83444-136">Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="83444-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="83444-137">Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.</span><span class="sxs-lookup"><span data-stu-id="83444-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>