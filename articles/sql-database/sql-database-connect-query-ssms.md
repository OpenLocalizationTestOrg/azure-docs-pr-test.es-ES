---
title: "SSMS: conexión y consulta de datos en Azure SQL Database | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconnect tooSQL la base de datos en Azure mediante el uso de SQL Server Management Studio (SSMS). A continuación, ejecute las instrucciones de Transact-SQL (T-SQL) tooquery y editar los datos."
metacanonical: 
keywords: "conectar la base de datos de toosql, studio de administración de sql server"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a>Base de datos SQL Azure: Use SQL Server Management Studio tooconnect y consultar datos

[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) es un entorno integrado para administrar cualquier infraestructura SQL, desde SQL Server tooSQL base de datos de Microsoft Windows. Este inicio rápido muestra la base de datos de toouse SSMS tooconnect tooan SQL Azure y, a continuación, tooquery de instrucciones de uso de Transact-SQL, insertan, actualizar y eliminar datos en la base de datos de Hola. 

## <a name="prerequisites"></a>Requisitos previos

Esta guía de inicio rápido se usa como sus recursos de hello punto inicial creados mediante uno de estos tutoriales:

- [Creación de la base de datos: Azure Portal](sql-database-get-started-portal.md)
- [Creación de la base de datos: CLI](sql-database-get-started-cli.md)
- [Creación de la base de datos: PowerShell](sql-database-get-started-powershell.md)

Antes de empezar, asegúrese de que ha instalado la versión más reciente de Hola de [SSMS](https://msdn.microsoft.com/library/mt238290.aspx). 

## <a name="sql-server-connection-information"></a>Información de conexión de SQL server

Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria. Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 
3. En hello **Introducción** página de la base de datos, revise el nombre del servidor de acceso completa de hello tal y como se muestra en la imagen de hello siguiente. Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.

   ![información sobre la conexión](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si ha olvidado la información de inicio de sesión de hello para el servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola. 

## <a name="connect-tooyour-database"></a>Conectar la base de datos de tooyour

Usar SQL Server Management Studio tooestablish un servidor de base de datos de SQL Azure tooyour de conexión. 

> [!IMPORTANT]
> Un servidor lógico de Azure SQL Database escucha en el puerto 1433. Si estás intentando tooconnect tooan base de datos de SQL Azure servidor lógico desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo hello para la conexión se toosuccessfully.
>

1. Abra SQL Server Management Studio.

2. Hola **conectar tooServer** diálogo cuadro, escriba Hola siguiente información:

   | Configuración       | Valor sugerido | Descripción | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | nombre completo del servidor de Hola | Hello nombre debe ser algo parecido a esto: **mynewserver20170313.database.windows.net**. |
   | **Autenticación** | Autenticación de SQL Server | Autenticación de SQL es Hola único tipo de autenticación que hemos configurado en este tutorial. |
   | **Inicio de sesión** | cuenta de administrador del servidor de Hola | Esta es la cuenta de hello que especificó cuando creó el servidor de Hola. |
   | **Password** | contraseña de Hello para la cuenta de administrador del servidor | Esta es la contraseña de Hola que especificó cuando creó el servidor de Hola. |

   ![conectar tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. Haga clic en **opciones** en hello **conectar tooserver** cuadro de diálogo. Hola **conectar toodatabase** sección, escriba **mySampleDatabase** base de datos de tooconnect toothis.

   ![conectar toodb en servidor](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Haga clic en **Conectar**. Abre la ventana del explorador de objetos de Hello en SSMS. 

   ![tooserver conectado](./media/sql-database-connect-query-ssms/connected.png)  

5. En el Explorador de objetos, expanda **bases de datos** y, a continuación, expanda **mySampleDatabase** tooview objetos de hello en la base de datos de ejemplo de Hola.

## <a name="query-data"></a>Datos de consulta

Siguiente de Hola de uso de código tooquery para productos de hello 20 primeros por categoría con hello [seleccione](https://msdn.microsoft.com/library/ms189499.aspx) instrucción Transact-SQL.

1. En el Explorador de objetos, haga clic con el botón derecho en **mySampleDatabase** y luego en **Nueva consulta**. Abre una ventana de consulta en blanco que es conectado tooyour base de datos.
2. En la ventana de consulta de hello, escriba Hola después de consulta:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. En la barra de herramientas de hello, haga clic en **Execute** tooretrieve datos de tablas de Product y ProductCategory de Hola.

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a>Insertar datos

Use Hola siguiente de código tooinsert un nuevo producto en tabla de SalesLT.Product de hello mediante hello [insertar](https://msdn.microsoft.com/library/ms174335.aspx) instrucción Transact-SQL.

1. En la ventana de consulta de hello, reemplace consulta anterior Hola con hello después de consulta:

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. En la barra de herramientas de hello, haga clic en **Execute** tooinsert una nueva fila en la tabla de productos de Hola.

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a>Actualización de datos

Siguiente de Hola de uso de código que agregó anteriormente utilizando Hola de nuevo producto tooupdate hello [actualización](https://msdn.microsoft.com/library/ms177523.aspx) instrucción Transact-SQL.

1. En la ventana de consulta de hello, reemplace consulta anterior Hola con hello después de consulta:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. En la barra de herramientas de hello, haga clic en **Execute** fila especificada de hello tooupdate en la tabla de productos de Hola.

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a>Eliminación de datos

Siguiente de Hola de uso de código que agregó anteriormente utilizando Hola de nuevo producto toodelete hello [eliminar](https://msdn.microsoft.com/library/ms189835.aspx) instrucción Transact-SQL.

1. En la ventana de consulta de hello, reemplace consulta anterior Hola con hello después de consulta:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. En la barra de herramientas de hello, haga clic en **Execute** fila especificada de hello toodelete en la tabla de productos de Hola.

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a>Pasos siguientes

- toolearn sobre la creación y administración de servidores y bases de datos con Transact-SQL, consulte [más información acerca de los servidores de base de datos de SQL Azure y bases de datos](sql-database-servers-databases.md).
- Para más información acerca de SSMS, consulte [Uso de SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
- tooconnect y consulta mediante código de Visual Studio, vea [conectar y consultas con código de Visual Studio](sql-database-connect-query-vscode.md).
- tooconnect y consulta con. NET, vea [conectar y consultas con .NET](sql-database-connect-query-dotnet.md).
- tooconnect y consultas con PHP, consulte [conectar y consultas con PHP](sql-database-connect-query-php.md).
- tooconnect y consulta con Node.js, vea [conectar y consultas con Node.js](sql-database-connect-query-nodejs.md).
- tooconnect y consulta con Java, consulte [conectar y consultas con Java](sql-database-connect-query-java.md).
- tooconnect y consultas con Python, consulte [conectar y consultas con Python](sql-database-connect-query-python.md).
- tooconnect y consulta con Ruby, vea [conectar y consultas con Ruby](sql-database-connect-query-ruby.md).
