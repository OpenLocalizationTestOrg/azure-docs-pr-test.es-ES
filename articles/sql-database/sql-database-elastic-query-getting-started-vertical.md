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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Introducción a las consultas entre bases de datos (particiones verticales) (versión preliminar)
Consulta de base de datos elástica (versión preliminar) para la base de datos de SQL Azure le permite toorun consultas de T-SQL que abarcan varias bases de datos con un punto de conexión. En este tema se aplica demasiado[dividido verticalmente las bases de datos](sql-database-elastic-query-vertical-partitioning.md).  

Cuando haya completado, tendrá que: Obtenga información acerca de cómo tooconfigure y usar una base de datos de SQL Azure tooperform las consultas que usan varias bases de datos relacionadas. 

Para obtener más información acerca de la característica de consulta de base de datos elástica hello, visite [información general sobre la consulta de base de datos elástica de base de datos de SQL Azure](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Requisitos previos

Se debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE. Este permiso se incluye con el permiso ALTER DATABASE Hola. Los permisos ALTER ANY EXTERNAL DATA SOURCE son toohello toorefer necesario el origen de datos subyacentes.

## <a name="create-hello-sample-databases"></a>Crear bases de datos de ejemplo de Hola
toostart con, necesitamos toocreate dos bases de datos, **clientes** y **pedidos**, ya sea en Hola iguales o distintos servidores lógicos.   

Ejecute hello las siguientes consultas en hello **pedidos** Hola de base de datos toocreate **Informacióndepedido** tabla y entrada de datos de ejemplo de Hola. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Ahora, ejecute la consulta en hello siguiente **clientes** Hola de base de datos toocreate **Informacióndecliente** tabla y entrada de datos de ejemplo de Hola. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Creación de objetos de base de datos
### <a name="database-scoped-master-key-and-credentials"></a>Clave maestra y credenciales de ámbito de base de datos
1. Abra SQL Server Management Studio o SQL Server Data Tools en Visual Studio.
2. Conectar la base de datos de pedidos de toohello y ejecute hello siga los comandos del código T-SQL:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Hola "username" y "password" deben ser el nombre de usuario de Hola y contraseña utilizados toologin en base de datos de los clientes de Hola.
    Actualmente no se admite la autenticación usando Azure Active Directory con consultas elásticas.

### <a name="external-data-sources"></a>Orígenes de datos externos
toocreate un origen de datos externo, ejecute hello siguiente comando en la base de datos de pedidos de hello: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Tablas externas
Crear una tabla externa en hello pedidos base de datos que coincide con la definición de Hola de tabla de hello Informacióndecliente:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Ejecución de la consulta de T-SQL de la base de datos elástica de ejemplo
Una vez que haya definido el origen de datos externo y las tablas externas ahora puede usar las tablas externas tooquery de T-SQL. Ejecute esta consulta en la base de datos de pedidos de hello: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Coste
Actualmente, característica de consulta de base de datos elástica Hola se incluye en el costo de saludo de la base de datos de SQL Azure.  

Para obtener información de precios, vea [Precio de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)
* Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.