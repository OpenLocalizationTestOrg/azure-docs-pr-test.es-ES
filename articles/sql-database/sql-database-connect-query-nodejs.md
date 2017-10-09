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
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="225b0-103">Usar Node.js tooquery una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="225b0-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="225b0-104">Este tutorial de inicio rápido se muestra cómo toouse [Node.js](https://nodejs.org/en/) toocreate un tooan de tooconnect programa SQL Azure la base de datos y usar datos de tooquery de instrucciones de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="225b0-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="225b0-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="225b0-105">Prerequisites</span></span>

<span data-ttu-id="225b0-106">toocomplete rápida de este tutorial de inicio, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="225b0-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="225b0-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="225b0-107">An Azure SQL database.</span></span> <span data-ttu-id="225b0-108">Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="225b0-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="225b0-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="225b0-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="225b0-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="225b0-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="225b0-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="225b0-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="225b0-112">A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="225b0-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="225b0-113">Ha instalado Node.js y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="225b0-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="225b0-114">**MacOS**: instalar Homebrew y Node.js y, a continuación, instalar el controlador ODBC de Hola y SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="225b0-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="225b0-115">Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="225b0-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="225b0-116">**Ubuntu**: instalar Node.js y, a continuación, instalar el controlador ODBC de Hola y SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="225b0-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="225b0-117">Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="225b0-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="225b0-118">**Windows**: instale Chocolatey y Node.js y, a continuación, instale el controlador ODBC de Hola y SQL CMD.</span><span class="sxs-lookup"><span data-stu-id="225b0-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="225b0-119">Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="225b0-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="225b0-120">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="225b0-120">SQL server connection information</span></span>

<span data-ttu-id="225b0-121">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="225b0-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="225b0-122">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="225b0-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="225b0-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="225b0-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="225b0-124">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="225b0-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="225b0-125">En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="225b0-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="225b0-126">Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.</span><span class="sxs-lookup"><span data-stu-id="225b0-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="225b0-128">Si ha olvidado la información de inicio de sesión de hello para el servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="225b0-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="225b0-129">Debe tener una regla de firewall en su lugar para la dirección IP pública de hello del equipo de hello en el que realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="225b0-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="225b0-130">Si se encuentran en un equipo diferente o tiene una dirección IP pública diferentes, cree un [regla de firewall de nivel de servidor mediante Hola portal de Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="225b0-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="225b0-131">Creación de un proyecto Node.js</span><span class="sxs-lookup"><span data-stu-id="225b0-131">Create a Node.js project</span></span>

<span data-ttu-id="225b0-132">Abra un símbolo del sistema y cree una carpeta denominada *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="225b0-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="225b0-133">Desplazarse por las carpetas de toohello que creó y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="225b0-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="225b0-134">Insertar la base de datos SQL de tooquery de código</span><span class="sxs-lookup"><span data-stu-id="225b0-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="225b0-135">En el entorno de desarrollo o en el editor de texto, cree un nuevo archivo, **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="225b0-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="225b0-136">Reemplace el contenido de hello con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="225b0-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="225b0-137">Ejecutar código de hello</span><span class="sxs-lookup"><span data-stu-id="225b0-137">Run hello code</span></span>

1. <span data-ttu-id="225b0-138">En hello símbolo del sistema, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="225b0-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="225b0-139">Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="225b0-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="225b0-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="225b0-140">Next steps</span></span>

- <span data-ttu-id="225b0-141">Obtenga información acerca de hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="225b0-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="225b0-142">Obtenga información acerca de cómo demasiado[conectarse y consultar una base de datos de SQL Azure mediante .NET core](sql-database-connect-query-dotnet-core.md) en Windows/Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="225b0-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="225b0-143">Obtenga información acerca de [Introducción a .NET Core en Windows/Linux/macOS mediante la línea de comandos de hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="225b0-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="225b0-144">Obtenga información acerca de cómo demasiado[diseñar la primera base de datos de SQL Azure con SSMS](sql-database-design-first-database.md) o [diseñar la primera base de datos de SQL Azure mediante .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="225b0-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="225b0-145">Obtenga información acerca de cómo demasiado[Connect y consultas con SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="225b0-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="225b0-146">Obtenga información acerca de cómo demasiado[conectar y consultas con código de Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="225b0-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


