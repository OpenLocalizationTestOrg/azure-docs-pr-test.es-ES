---
title: Uso de PHP para consultar Azure SQL Database | Microsoft Docs
description: "En este tema se muestra cómo usar PHP para crear un programa que se conecta a una base de datos SQL de Azure y realiza consultas mediante instrucciones Transact-SQL."
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
ms.openlocfilehash: 3a43472ad2be4a0fd6f7126f72433acd8b5f25fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-php-to-query-an-azure-sql-database"></a><span data-ttu-id="f078c-103">Uso de PHP para consultar una base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="f078c-103">Use PHP to query an Azure SQL database</span></span>

<span data-ttu-id="f078c-104">Este tutorial de introducción muestra cómo usar [PHP](http://php.net/manual/en/intro-whatis.php) para crear un programa que se conecta a una base de datos SQL de Azure y utiliza instrucciones Transact-SQL para consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="f078c-104">This quick start tutorial demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f078c-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f078c-105">Prerequisites</span></span>

<span data-ttu-id="f078c-106">Para completar este tutorial, asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f078c-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="f078c-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f078c-107">An Azure SQL database.</span></span> <span data-ttu-id="f078c-108">En esta guía de inicio rápido se utilizan como punto de partida los recursos creados en una de las siguientes guías:</span><span class="sxs-lookup"><span data-stu-id="f078c-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="f078c-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f078c-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="f078c-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="f078c-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="f078c-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="f078c-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="f078c-112">Una [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública del equipo que usa para seguir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f078c-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="f078c-113">Ha instalado PHP y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f078c-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="f078c-114">**MacOS**: instalación de Homebrew y PHP, instalación del controlador ODBC y SQLCMD y, a continuación, instalación del controlador PHP para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f078c-114">**MacOS**: Install Homebrew and PHP, install the ODBC driver and SQLCMD, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="f078c-115">Consulte los [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="f078c-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="f078c-116">**Ubuntu**: instalación de PHP y otros paquetes necesarios y, a continuación, instalación del controlador PHP para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f078c-116">**Ubuntu**:  Install PHP and other required packages, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="f078c-117">Consulte los [pasos 1.2 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="f078c-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="f078c-118">**Windows**: instalación de la versión más reciente de PHP para IIS Express, la versión más reciente de Microsoft Drivers para SQL Server en IIS Express, Chocolatey, el controlador ODBC y SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="f078c-118">**Windows**: Install the newest version of PHP for IIS Express, the newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, the ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="f078c-119">Consulte los [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="f078c-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="f078c-120">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="f078c-120">SQL server connection information</span></span>

<span data-ttu-id="f078c-121">Obtención de la información de conexión necesaria para conectarse a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f078c-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="f078c-122">En los procedimientos siguientes, necesitará el nombre completo del servidor, el nombre de la base de datos y la información de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f078c-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="f078c-123">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f078c-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f078c-124">Seleccione **Bases de datos SQL** en el menú de la izquierda y haga clic en la base de datos en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="f078c-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="f078c-125">En la página **Introducción** de la base de datos, revise el nombre completo del servidor tal como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="f078c-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="f078c-126">Mantenga el puntero sobre el nombre del servidor hasta que aparezca la opción **Haga clic para copiar**.</span><span class="sxs-lookup"><span data-stu-id="f078c-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="f078c-128">Si olvida la información de inicio de sesión del servidor, navegue hasta la página del servidor de SQL Database para ver el nombre de administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f078c-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="f078c-129">Inserción de código para consultar la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f078c-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="f078c-130">En el editor de texto, cree un nuevo archivo, **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="f078c-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="f078c-131">Reemplace el contenido con el código siguiente y agregue los valores adecuados para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f078c-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes the connection
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

## <a name="run-the-code"></a><span data-ttu-id="f078c-132">Ejecución del código</span><span class="sxs-lookup"><span data-stu-id="f078c-132">Run the code</span></span>

1. <span data-ttu-id="f078c-133">En el símbolo del sistema, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="f078c-133">At the command prompt, run the following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="f078c-134">Compruebe que se han devuelto las primeras 20 filas y, a continuación, cierre la ventana de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f078c-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f078c-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f078c-135">Next steps</span></span>
- [<span data-ttu-id="f078c-136">Diseño de su primera base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="f078c-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="f078c-137">Controladores de Microsoft para PHP para SQL Server</span><span class="sxs-lookup"><span data-stu-id="f078c-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="f078c-138">Informe de los problemas y realización de preguntas</span><span class="sxs-lookup"><span data-stu-id="f078c-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
