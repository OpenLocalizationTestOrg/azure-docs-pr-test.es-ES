---
title: "VS Code: conexión con Azure SQL Database y consulta de datos | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconnect tooSQL la base de datos en Azure mediante el uso de código de Visual Studio. A continuación, ejecute las instrucciones de Transact-SQL (T-SQL) tooquery y editar los datos."
metacanonical: 
keywords: conectar la base de datos de toosql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>Base de datos SQL Azure: Usar Visual Studio Code tooconnect y consultar datos

[Código de Visual Studio](https://code.visualstudio.com/docs) es un editor de código gráfica para Linux, Mac OS, y Windows que admita extensiones, incluidas Hola [mssql extensión](https://aka.ms/mssql-marketplace) para realizar consultas en Microsoft SQL Server, base de datos de SQL Azure y almacenamiento de datos SQL. Este inicio rápido muestra cómo toouse base de datos de Visual Studio Code tooconnect tooan SQL Azure y, a continuación, tooquery de instrucciones de uso de Transact-SQL, insertarán, actualización y eliminan datos en la base de datos de Hola.

## <a name="prerequisites"></a>Requisitos previos

Esta guía de inicio rápido se usa como sus recursos de hello punto inicial creados mediante uno de estos tutoriales:

- [Creación de la base de datos: Azure Portal](sql-database-get-started-portal.md)
- [Creación de la base de datos: CLI](sql-database-get-started-cli.md)
- [Creación de la base de datos: PowerShell](sql-database-get-started-powershell.md)

Antes de empezar, asegúrese de que ha instalado la versión más reciente de Hola de [código de Visual Studio](https://code.visualstudio.com/Download) y hello cargado [mssql extensión](https://aka.ms/mssql-marketplace). Para obtener instrucciones de instalación para la extensión de hello mssql, consulte [instalar VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) y vea [mssql para el código de Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

## <a name="configure-vs-code"></a>Configuración del código de VS 

### <a name="mac-os"></a>**Mac OS**
Para macOS, deberá tooinstall OpenSSL que es un requisito previo para DotNet Core esa extensión mssql utiliza. Abra su terminal y escriba Hola después comandos tooinstall **brew** y **OpenSSL**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

No se necesita ninguna configuración especial.

### <a name="windows"></a>**Windows**

No se necesita ninguna configuración especial.

## <a name="sql-server-connection-information"></a>Información de conexión de SQL server

Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria. Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 
3. En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen. Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.

   ![información sobre la conexión](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si ha olvidado la información de inicio de sesión de hello para el servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola. 

## <a name="set-language-mode-toosql"></a>Set language modo tooSQL

Establecer el modo de lenguaje de Hola se establece demasiado**SQL** de comandos de Visual Studio Code tooenable mssql e IntelliSense de T-SQL.

1. Abra una nueva ventana de Visual Studio Code. 

2. Haga clic en **texto sin formato** en hello inferior derecho de barra de estado de Hola.
3. Hola **modo Seleccionar idioma** menú desplegable que se abre, escriba **SQL**y, a continuación, presione **ENTRAR** tooset Hola lenguaje modo tooSQL. 

   ![Modo de lenguaje SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>Conectar la base de datos de tooyour

Usar un servidor de base de datos de SQL Azure tooyour de conexión del código de Visual Studio tooestablish.

> [!IMPORTANT]
> Antes de continuar, asegúrese de que están preparados el servidor, la base de datos y la lista de información de inicio de sesión. Una vez iniciada la introducir información de perfil de conexión de hello, si cambia el foco de código de Visual Studio, tiene toorestart Crear perfil de conexión de Hola.
>

1. En el código de VS, presione **CTRL + MAYÚS + P** (o **F1**) tooopen Hola paleta de comando.

2. Escriba **sqlcon** y presione **ENTRAR**.

3. Presione **ENTRAR** tooselect **Crear perfil de conexión**. Al hacerlo, se creará un perfil de conexión para la instancia de SQL Server.

4. Seguir propiedades de conexión de hello indicaciones toospecify Hola Hola nuevo perfil de conexión. Después de especificar cada valor, presione **ENTRAR** toocontinue. 

   | Configuración       | Valor sugerido | Descripción |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre de servidor | nombre completo del servidor de Hola | Hello nombre debe ser algo parecido a esto: **mynewserver20170313.database.windows.net**. |
   | **Nombre de la base de datos** | mySampleDatabase | nombre de Hola de hello base de datos toowhich tooconnect. |
   | **Autenticación** | Inicio de sesión SQL| Autenticación de SQL es Hola único tipo de autenticación que hemos configurado en este tutorial. |
   | **Nombre de usuario** | cuenta de administrador del servidor de Hola | Esta es la cuenta de hello que especificó cuando creó el servidor de Hola. |
   | **Contraseña (Inicio de sesión de SQL)** | contraseña de Hello para la cuenta de administrador del servidor | Esta es la contraseña de Hola que especificó cuando creó el servidor de Hola. |
   | **¿Guardar la contraseña?** | Sí o no | Seleccione Sí si no desea tooenter Hola contraseña cada vez. |
   | **Escribir un nombre para este perfil** | Un nombre de perfil, como **mySampleDatabase** | Un nombre de perfil guardado acelera la conexión en los inicios de sesión posteriores. | 

5. Hola presione **ESC** mensaje de información de hello tooclose clave que le informa que hemos creado el perfil de Hola y conectado.

6. Compruebe la conexión en la barra de estado de Hola.

   ![Estado de la conexión](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>Datos de consulta

Siguiente de Hola de uso de código tooquery para productos de hello 20 primeros por categoría con hello [seleccione](https://msdn.microsoft.com/library/ms189499.aspx) instrucción Transact-SQL.

1. Hola **Editor** ventana, escriba Hola después de consulta en la ventana de consulta vacía hello:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. Presione **CTRL + MAYÚS + E** tooretrieve datos de tablas de Product y ProductCategory de Hola.

    ![Consultar](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>Insertar datos

Use Hola siguiente de código tooinsert un nuevo producto en tabla de SalesLT.Product de hello mediante hello [insertar](https://msdn.microsoft.com/library/ms174335.aspx) instrucción Transact-SQL.

1. Hola **Editor** ventana, eliminar la consulta anterior hello y escriba Hola después de consulta:

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

2. Presione **CTRL + MAYÚS + E** tooinsert una nueva fila en la tabla de productos de Hola.

## <a name="update-data"></a>Actualización de datos

Siguiente de Hola de uso de código que agregó anteriormente utilizando Hola de nuevo producto tooupdate hello [actualización](https://msdn.microsoft.com/library/ms177523.aspx) instrucción Transact-SQL.

1.  Hola **Editor** ventana, eliminar la consulta anterior hello y escriba Hola después de consulta:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Presione **CTRL + MAYÚS + E** fila especificada de hello tooupdate en la tabla de productos de Hola.

## <a name="delete-data"></a>Eliminación de datos

Siguiente de Hola de uso de código que agregó anteriormente utilizando Hola de nuevo producto toodelete hello [eliminar](https://msdn.microsoft.com/library/ms189835.aspx) instrucción Transact-SQL.

1. Hola **Editor** ventana, eliminar la consulta anterior hello y escriba Hola después de consulta:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Presione **CTRL + MAYÚS + E** fila especificada de hello toodelete en la tabla de productos de Hola.

## <a name="next-steps"></a>Pasos siguientes

- tooconnect y consulta utilizando SQL Server Management Studio, vea [conectar y consultas con SSMS](sql-database-connect-query-ssms.md).
- Si está interesado en ver un artículo de la revista de MSDN sobre el uso de Visual Studio Code, consulte la entrada del blob sobre cómo [crear un IDE de base de datos con la extensión MSSQL](https://msdn.microsoft.com/magazine/mt809115).
