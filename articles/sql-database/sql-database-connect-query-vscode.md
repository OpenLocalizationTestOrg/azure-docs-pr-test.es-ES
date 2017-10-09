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
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a><span data-ttu-id="90da7-105">Base de datos SQL Azure: Usar Visual Studio Code tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="90da7-105">Azure SQL Database: Use Visual Studio Code tooconnect and query data</span></span>

<span data-ttu-id="90da7-106">[Código de Visual Studio](https://code.visualstudio.com/docs) es un editor de código gráfica para Linux, Mac OS, y Windows que admita extensiones, incluidas Hola [mssql extensión](https://aka.ms/mssql-marketplace) para realizar consultas en Microsoft SQL Server, base de datos de SQL Azure y almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="90da7-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="90da7-107">Este inicio rápido muestra cómo toouse base de datos de Visual Studio Code tooconnect tooan SQL Azure y, a continuación, tooquery de instrucciones de uso de Transact-SQL, insertarán, actualización y eliminan datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-107">This quick start demonstrates how toouse Visual Studio Code tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90da7-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="90da7-108">Prerequisites</span></span>

<span data-ttu-id="90da7-109">Esta guía de inicio rápido se usa como sus recursos de hello punto inicial creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="90da7-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="90da7-110">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="90da7-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="90da7-111">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="90da7-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="90da7-112">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="90da7-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="90da7-113">Antes de empezar, asegúrese de que ha instalado la versión más reciente de Hola de [código de Visual Studio](https://code.visualstudio.com/Download) y hello cargado [mssql extensión](https://aka.ms/mssql-marketplace).</span><span class="sxs-lookup"><span data-stu-id="90da7-113">Before you start, make sure you have installed hello newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded hello [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="90da7-114">Para obtener instrucciones de instalación para la extensión de hello mssql, consulte [instalar VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) y vea [mssql para el código de Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span><span class="sxs-lookup"><span data-stu-id="90da7-114">For installation guidance for hello mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="90da7-115">Configuración del código de VS</span><span class="sxs-lookup"><span data-stu-id="90da7-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="90da7-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="90da7-116">**Mac OS**</span></span>
<span data-ttu-id="90da7-117">Para macOS, deberá tooinstall OpenSSL que es un requisito previo para DotNet Core esa extensión mssql utiliza.</span><span class="sxs-lookup"><span data-stu-id="90da7-117">For macOS, you need tooinstall OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="90da7-118">Abra su terminal y escriba Hola después comandos tooinstall **brew** y **OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="90da7-118">Open your terminal and enter hello following commands tooinstall **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="90da7-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="90da7-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="90da7-120">No se necesita ninguna configuración especial.</span><span class="sxs-lookup"><span data-stu-id="90da7-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="90da7-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="90da7-121">**Windows**</span></span>

<span data-ttu-id="90da7-122">No se necesita ninguna configuración especial.</span><span class="sxs-lookup"><span data-stu-id="90da7-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="90da7-123">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="90da7-123">SQL server connection information</span></span>

<span data-ttu-id="90da7-124">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="90da7-124">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="90da7-125">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-125">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="90da7-126">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90da7-126">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90da7-127">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="90da7-127">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="90da7-128">En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="90da7-128">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="90da7-129">Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.</span><span class="sxs-lookup"><span data-stu-id="90da7-129">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![información sobre la conexión](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="90da7-131">Si ha olvidado la información de inicio de sesión de hello para el servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-131">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="set-language-mode-toosql"></a><span data-ttu-id="90da7-132">Set language modo tooSQL</span><span class="sxs-lookup"><span data-stu-id="90da7-132">Set language mode tooSQL</span></span>

<span data-ttu-id="90da7-133">Establecer el modo de lenguaje de Hola se establece demasiado**SQL** de comandos de Visual Studio Code tooenable mssql e IntelliSense de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="90da7-133">Set hello language mode is set too**SQL** in Visual Studio Code tooenable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="90da7-134">Abra una nueva ventana de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="90da7-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="90da7-135">Haga clic en **texto sin formato** en hello inferior derecho de barra de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-135">Click **Plain Text** in hello lower right-hand corner of hello status bar.</span></span>
3. <span data-ttu-id="90da7-136">Hola **modo Seleccionar idioma** menú desplegable que se abre, escriba **SQL**y, a continuación, presione **ENTRAR** tooset Hola lenguaje modo tooSQL.</span><span class="sxs-lookup"><span data-stu-id="90da7-136">In hello **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** tooset hello language mode tooSQL.</span></span> 

   ![Modo de lenguaje SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a><span data-ttu-id="90da7-138">Conectar la base de datos de tooyour</span><span class="sxs-lookup"><span data-stu-id="90da7-138">Connect tooyour database</span></span>

<span data-ttu-id="90da7-139">Usar un servidor de base de datos de SQL Azure tooyour de conexión del código de Visual Studio tooestablish.</span><span class="sxs-lookup"><span data-stu-id="90da7-139">Use Visual Studio Code tooestablish a connection tooyour Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90da7-140">Antes de continuar, asegúrese de que están preparados el servidor, la base de datos y la lista de información de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="90da7-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="90da7-141">Una vez iniciada la introducir información de perfil de conexión de hello, si cambia el foco de código de Visual Studio, tiene toorestart Crear perfil de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-141">Once you begin entering hello connection profile information, if you change your focus from Visual Studio Code, you have toorestart creating hello connection profile.</span></span>
>

1. <span data-ttu-id="90da7-142">En el código de VS, presione **CTRL + MAYÚS + P** (o **F1**) tooopen Hola paleta de comando.</span><span class="sxs-lookup"><span data-stu-id="90da7-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) tooopen hello Command Palette.</span></span>

2. <span data-ttu-id="90da7-143">Escriba **sqlcon** y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="90da7-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="90da7-144">Presione **ENTRAR** tooselect **Crear perfil de conexión**.</span><span class="sxs-lookup"><span data-stu-id="90da7-144">Press **ENTER** tooselect **Create Connection Profile**.</span></span> <span data-ttu-id="90da7-145">Al hacerlo, se creará un perfil de conexión para la instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="90da7-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="90da7-146">Seguir propiedades de conexión de hello indicaciones toospecify Hola Hola nuevo perfil de conexión.</span><span class="sxs-lookup"><span data-stu-id="90da7-146">Follow hello prompts toospecify hello connection properties for hello new connection profile.</span></span> <span data-ttu-id="90da7-147">Después de especificar cada valor, presione **ENTRAR** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="90da7-147">After specifying each value, press **ENTER** toocontinue.</span></span> 

   | <span data-ttu-id="90da7-148">Configuración</span><span class="sxs-lookup"><span data-stu-id="90da7-148">Setting</span></span>       | <span data-ttu-id="90da7-149">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="90da7-149">Suggested value</span></span> | <span data-ttu-id="90da7-150">Descripción</span><span class="sxs-lookup"><span data-stu-id="90da7-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="90da7-151">**Nombre de servidor</span><span class="sxs-lookup"><span data-stu-id="90da7-151">**Server name</span></span> | <span data-ttu-id="90da7-152">nombre completo del servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="90da7-152">hello fully qualified server name</span></span> | <span data-ttu-id="90da7-153">Hello nombre debe ser algo parecido a esto: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="90da7-153">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="90da7-154">**Nombre de la base de datos**</span><span class="sxs-lookup"><span data-stu-id="90da7-154">**Database name**</span></span> | <span data-ttu-id="90da7-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="90da7-155">mySampleDatabase</span></span> | <span data-ttu-id="90da7-156">nombre de Hola de hello base de datos toowhich tooconnect.</span><span class="sxs-lookup"><span data-stu-id="90da7-156">hello name of hello database toowhich tooconnect.</span></span> |
   | <span data-ttu-id="90da7-157">**Autenticación**</span><span class="sxs-lookup"><span data-stu-id="90da7-157">**Authentication**</span></span> | <span data-ttu-id="90da7-158">Inicio de sesión SQL</span><span class="sxs-lookup"><span data-stu-id="90da7-158">SQL Login</span></span>| <span data-ttu-id="90da7-159">Autenticación de SQL es Hola único tipo de autenticación que hemos configurado en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="90da7-159">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="90da7-160">**Nombre de usuario**</span><span class="sxs-lookup"><span data-stu-id="90da7-160">**User name**</span></span> | <span data-ttu-id="90da7-161">cuenta de administrador del servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="90da7-161">hello server admin account</span></span> | <span data-ttu-id="90da7-162">Esta es la cuenta de hello que especificó cuando creó el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-162">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="90da7-163">**Contraseña (Inicio de sesión de SQL)**</span><span class="sxs-lookup"><span data-stu-id="90da7-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="90da7-164">contraseña de Hello para la cuenta de administrador del servidor</span><span class="sxs-lookup"><span data-stu-id="90da7-164">hello password for your server admin account</span></span> | <span data-ttu-id="90da7-165">Esta es la contraseña de Hola que especificó cuando creó el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-165">This is hello password that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="90da7-166">**¿Guardar la contraseña?**</span><span class="sxs-lookup"><span data-stu-id="90da7-166">**Save Password?**</span></span> | <span data-ttu-id="90da7-167">Sí o no</span><span class="sxs-lookup"><span data-stu-id="90da7-167">Yes or No</span></span> | <span data-ttu-id="90da7-168">Seleccione Sí si no desea tooenter Hola contraseña cada vez.</span><span class="sxs-lookup"><span data-stu-id="90da7-168">Select Yes if you do not want tooenter hello password each time.</span></span> |
   | <span data-ttu-id="90da7-169">**Escribir un nombre para este perfil**</span><span class="sxs-lookup"><span data-stu-id="90da7-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="90da7-170">Un nombre de perfil, como **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="90da7-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="90da7-171">Un nombre de perfil guardado acelera la conexión en los inicios de sesión posteriores.</span><span class="sxs-lookup"><span data-stu-id="90da7-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="90da7-172">Hola presione **ESC** mensaje de información de hello tooclose clave que le informa que hemos creado el perfil de Hola y conectado.</span><span class="sxs-lookup"><span data-stu-id="90da7-172">Press hello **ESC** key tooclose hello info message that informs you that hello profile is created and connected.</span></span>

6. <span data-ttu-id="90da7-173">Compruebe la conexión en la barra de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-173">Verify your connection in hello status bar.</span></span>

   ![Estado de la conexión](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="90da7-175">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="90da7-175">Query data</span></span>

<span data-ttu-id="90da7-176">Siguiente de Hola de uso de código tooquery para productos de hello 20 primeros por categoría con hello [seleccione](https://msdn.microsoft.com/library/ms189499.aspx) instrucción Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="90da7-176">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="90da7-177">Hola **Editor** ventana, escriba Hola después de consulta en la ventana de consulta vacía hello:</span><span class="sxs-lookup"><span data-stu-id="90da7-177">In hello **Editor** window, enter hello following query in hello empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="90da7-178">Presione **CTRL + MAYÚS + E** tooretrieve datos de tablas de Product y ProductCategory de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-178">Press **CTRL+SHIFT+E** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![Consultar](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="90da7-180">Insertar datos</span><span class="sxs-lookup"><span data-stu-id="90da7-180">Insert data</span></span>

<span data-ttu-id="90da7-181">Use Hola siguiente de código tooinsert un nuevo producto en tabla de SalesLT.Product de hello mediante hello [insertar](https://msdn.microsoft.com/library/ms174335.aspx) instrucción Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="90da7-181">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="90da7-182">Hola **Editor** ventana, eliminar la consulta anterior hello y escriba Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="90da7-182">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

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

2. <span data-ttu-id="90da7-183">Presione **CTRL + MAYÚS + E** tooinsert una nueva fila en la tabla de productos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-183">Press **CTRL+SHIFT+E** tooinsert a new row in hello Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="90da7-184">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="90da7-184">Update data</span></span>

<span data-ttu-id="90da7-185">Siguiente de Hola de uso de código que agregó anteriormente utilizando Hola de nuevo producto tooupdate hello [actualización](https://msdn.microsoft.com/library/ms177523.aspx) instrucción Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="90da7-185">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="90da7-186">Hola **Editor** ventana, eliminar la consulta anterior hello y escriba Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="90da7-186">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="90da7-187">Presione **CTRL + MAYÚS + E** fila especificada de hello tooupdate en la tabla de productos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-187">Press **CTRL+SHIFT+E** tooupdate hello specified row in hello Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="90da7-188">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="90da7-188">Delete data</span></span>

<span data-ttu-id="90da7-189">Siguiente de Hola de uso de código que agregó anteriormente utilizando Hola de nuevo producto toodelete hello [eliminar](https://msdn.microsoft.com/library/ms189835.aspx) instrucción Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="90da7-189">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="90da7-190">Hola **Editor** ventana, eliminar la consulta anterior hello y escriba Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="90da7-190">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="90da7-191">Presione **CTRL + MAYÚS + E** fila especificada de hello toodelete en la tabla de productos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90da7-191">Press **CTRL+SHIFT+E** toodelete hello specified row in hello Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90da7-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90da7-192">Next steps</span></span>

- <span data-ttu-id="90da7-193">tooconnect y consulta utilizando SQL Server Management Studio, vea [conectar y consultas con SSMS](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="90da7-193">tooconnect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="90da7-194">Si está interesado en ver un artículo de la revista de MSDN sobre el uso de Visual Studio Code, consulte la entrada del blob sobre cómo [crear un IDE de base de datos con la extensión MSSQL](https://msdn.microsoft.com/magazine/mt809115).</span><span class="sxs-lookup"><span data-stu-id="90da7-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
