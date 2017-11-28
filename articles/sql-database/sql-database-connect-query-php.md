---
title: aaaUse PHP tooquery base de datos de SQL de Azure | Documentos de Microsoft
description: "Este tema muestra cómo toouse PHP toocreate un programa que conecta tooan base de datos de SQL Azure y consultas mediante instrucciones Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="856f8-103">Usar PHP tooquery una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="856f8-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="856f8-104">Este tutorial de inicio rápido se muestra cómo toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate un tooan de tooconnect programa SQL Azure la base de datos y usar datos de tooquery de instrucciones de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="856f8-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="856f8-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="856f8-105">Prerequisites</span></span>

<span data-ttu-id="856f8-106">toocomplete rápida de este tutorial de inicio, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="856f8-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="856f8-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="856f8-107">An Azure SQL database.</span></span> <span data-ttu-id="856f8-108">Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="856f8-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="856f8-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="856f8-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="856f8-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="856f8-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="856f8-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="856f8-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="856f8-112">A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="856f8-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="856f8-113">Ha instalado PHP y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="856f8-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="856f8-114">**MacOS**: Homebrew instalar PHP, instale el controlador ODBC de Hola y SQLCMD y, a continuación, instale Hola controlador PHP para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="856f8-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="856f8-115">Consulte los [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="856f8-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="856f8-116">**Ubuntu**: instalar PHP y otros necesarios paquetes y, a continuación, Hola instalar controladores de PHP para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="856f8-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="856f8-117">Consulte los [pasos 1.2 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="856f8-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="856f8-118">**Windows**: versión más reciente de Hola de instalación de PHP para IIS Express, versión más reciente de Hola de Microsoft Drivers para SQL Server en IIS Express, Chocolatey, el controlador ODBC de Hola y SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="856f8-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="856f8-119">Consulte los [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="856f8-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="856f8-120">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="856f8-120">SQL server connection information</span></span>

<span data-ttu-id="856f8-121">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="856f8-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="856f8-122">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="856f8-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="856f8-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="856f8-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="856f8-124">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="856f8-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="856f8-125">En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="856f8-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="856f8-126">Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.</span><span class="sxs-lookup"><span data-stu-id="856f8-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="856f8-128">Si olvida su información de inicio de sesión de servidor, vaya toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="856f8-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="856f8-129">Insertar la base de datos SQL de tooquery de código</span><span class="sxs-lookup"><span data-stu-id="856f8-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="856f8-130">En el editor de texto, cree un nuevo archivo, **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="856f8-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="856f8-131">Reemplace el contenido de hello con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="856f8-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a><span data-ttu-id="856f8-132">Ejecutar código de hello</span><span class="sxs-lookup"><span data-stu-id="856f8-132">Run hello code</span></span>

1. <span data-ttu-id="856f8-133">En hello símbolo del sistema, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="856f8-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="856f8-134">Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="856f8-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="856f8-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="856f8-135">Next steps</span></span>
- [<span data-ttu-id="856f8-136">Diseño de su primera base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="856f8-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="856f8-137">Controladores de Microsoft para PHP para SQL Server</span><span class="sxs-lookup"><span data-stu-id="856f8-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="856f8-138">Informe de los problemas y realización de preguntas</span><span class="sxs-lookup"><span data-stu-id="856f8-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
