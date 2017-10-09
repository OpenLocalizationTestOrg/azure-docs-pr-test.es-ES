---
title: aaaUse Node.js tooquery base de datos de SQL de Azure | Documentos de Microsoft
description: "Este tema muestra cómo toouse Node.js toocreate un programa que conecta tooan base de datos de SQL Azure y consultas mediante instrucciones Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a>Usar Node.js tooquery una base de datos de SQL Azure

Este tutorial de inicio rápido se muestra cómo toouse [Node.js](https://nodejs.org/en/) toocreate un tooan de tooconnect programa SQL Azure la base de datos y usar datos de tooquery de instrucciones de Transact-SQL.

## <a name="prerequisites"></a>Requisitos previos

toocomplete rápida de este tutorial de inicio, asegúrese de que tiene Hola siguientes:

- Una base de datos SQL de Azure. Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales: 

   - [Creación de la base de datos: Azure Portal](sql-database-get-started-portal.md)
   - [Creación de la base de datos: CLI](sql-database-get-started-cli.md)
   - [Creación de la base de datos: PowerShell](sql-database-get-started-powershell.md)

- A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.
- Ha instalado Node.js y el software relacionado para el sistema operativo.
    - **MacOS**: instalar Homebrew y Node.js y, a continuación, instalar el controlador ODBC de Hola y SQLCMD. Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).
    - **Ubuntu**: instalar Node.js y, a continuación, instalar el controlador ODBC de Hola y SQLCMD. Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).
    - **Windows**: instale Chocolatey y Node.js y, a continuación, instale el controlador ODBC de Hola y SQL CMD. Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).

## <a name="sql-server-connection-information"></a>Información de conexión de SQL server

Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria. Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 
3. En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen. Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si ha olvidado la información de inicio de sesión de hello para el servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola.

> [!IMPORTANT]
> Debe tener una regla de firewall en su lugar para la dirección IP pública de hello del equipo de hello en el que realizar este tutorial. Si se encuentran en un equipo diferente o tiene una dirección IP pública diferentes, cree un [regla de firewall de nivel de servidor mediante Hola portal de Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="create-a-nodejs-project"></a>Creación de un proyecto Node.js

Abra un símbolo del sistema y cree una carpeta denominada *sqltest*. Desplazarse por las carpetas de toohello que creó y ejecute el siguiente comando de hello:

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a>Insertar la base de datos SQL de tooquery de código

1. En el entorno de desarrollo o en el editor de texto, cree un nuevo archivo, **sqltest.js**.

2. Reemplace el contenido de hello con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt tooconnect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from hello Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-hello-code"></a>Ejecutar código de hello

1. En hello símbolo del sistema, ejecute hello siguientes comandos:

   ```js
   node sqltest.js
   ```

2. Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)
- Obtenga información acerca de cómo demasiado[conectarse y consultar una base de datos de SQL Azure mediante .NET core](sql-database-connect-query-dotnet-core.md) en Windows/Linux/macOS.  
- Obtenga información acerca de [Introducción a .NET Core en Windows/Linux/macOS mediante la línea de comandos de hello](/dotnet/core/tutorials/using-with-xplat-cli).
- Obtenga información acerca de cómo demasiado[diseñar la primera base de datos de SQL Azure con SSMS](sql-database-design-first-database.md) o [diseñar la primera base de datos de SQL Azure mediante .NET](sql-database-design-first-database-csharp.md).
- Obtenga información acerca de cómo demasiado[Connect y consultas con SSMS](sql-database-connect-query-ssms.md)
- Obtenga información acerca de cómo demasiado[conectar y consultas con código de Visual Studio](sql-database-connect-query-vscode.md).


