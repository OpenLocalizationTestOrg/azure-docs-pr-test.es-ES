---
title: "Conexión a Azure Database for PostgreSQL mediante PHP | Microsoft Docs"
description: "En este tutorial rápido se proporciona un ejemplo de código de PHP que puede usar para conectarse a Azure Database for PostgreSQL y consultar datos en este servicio."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: ed7c92e0689bca4056401d562271e3b6b7144dcf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a><span data-ttu-id="1e241-103">Azure Database for PostgreSQL: uso de PHP para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="1e241-103">Azure Database for PostgreSQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="1e241-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for PostgreSQL mediante una aplicación de [PHP](http://php.net/manual/intro-whatis.php).</span><span class="sxs-lookup"><span data-stu-id="1e241-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="1e241-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1e241-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="1e241-106">En este artículo se da por hecho que está familiarizado con el desarrollo mediante PHP, pero que nunca ha trabajado con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e241-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e241-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e241-107">Prerequisites</span></span>
<span data-ttu-id="1e241-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="1e241-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="1e241-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1e241-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="1e241-110">Creación de la base de datos: CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1e241-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="1e241-111">Instalación de PHP</span><span class="sxs-lookup"><span data-stu-id="1e241-111">Install PHP</span></span>
<span data-ttu-id="1e241-112">Instale PHP en su propio servidor o cree una [aplicación web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) de Azure que lo incluya.</span><span class="sxs-lookup"><span data-stu-id="1e241-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="1e241-113">Windows</span><span class="sxs-lookup"><span data-stu-id="1e241-113">Windows</span></span>
- <span data-ttu-id="1e241-114">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="1e241-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="1e241-115">Instale PHP y consulte el [manual de PHP](http://php.net/manual/install.windows.php) para continuar con la configuración.</span><span class="sxs-lookup"><span data-stu-id="1e241-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="1e241-116">El código usa la clase **pgsql** (ext/php_pgsql.dll) que se incluye en la instalación de PHP.</span><span class="sxs-lookup"><span data-stu-id="1e241-116">The code uses the **pgsql** class (ext/php_pgsql.dll)  that is included in the PHP installation.</span></span> 
- <span data-ttu-id="1e241-117">Ha habilitado la extensión **pgsql** mediante la edición del archivo de configuración php.ini, que normalmente se encuentra en `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="1e241-117">Enabled the **pgsql** extension by editing the php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="1e241-118">El archivo de configuración debe contener una línea con el texto `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="1e241-118">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="1e241-119">Si no se muestra, agregue el texto y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="1e241-119">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="1e241-120">Si el texto está presente, pero se ha comentado con un prefijo de punto y coma, quite el punto y coma para quitar la marca de comentario del texto.</span><span class="sxs-lookup"><span data-stu-id="1e241-120">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="1e241-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="1e241-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="1e241-122">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="1e241-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="1e241-123">Instale PHP y consulte el [manual de PHP](http://php.net/manual/install.unix.php) para continuar con la configuración.</span><span class="sxs-lookup"><span data-stu-id="1e241-123">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="1e241-124">El código usa la clase **pgsql** (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="1e241-124">The code uses the **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="1e241-125">Instálela mediante la ejecución de `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="1e241-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="1e241-126">Ha habilitado la extensión **pgsql** mediante la edición del archivo de configuración `/etc/php/7.0/mods-available/pgsql.ini`.</span><span class="sxs-lookup"><span data-stu-id="1e241-126">Enabled the **pgsql** extension by editing the `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="1e241-127">El archivo de configuración debe contener una línea con el texto `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="1e241-127">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="1e241-128">Si no se muestra, agregue el texto y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="1e241-128">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="1e241-129">Si el texto está presente, pero se ha comentado con un prefijo de punto y coma, quite el punto y coma para quitar la marca de comentario del texto.</span><span class="sxs-lookup"><span data-stu-id="1e241-129">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="1e241-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="1e241-130">MacOS</span></span>
- <span data-ttu-id="1e241-131">Descargue la [versión 7.1.4 de PHP](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="1e241-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="1e241-132">Instale PHP y consulte el [manual de PHP](http://php.net/manual/install.macosx.php) para continuar con la configuración.</span><span class="sxs-lookup"><span data-stu-id="1e241-132">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="1e241-133">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="1e241-133">Get connection information</span></span>
<span data-ttu-id="1e241-134">Obtenga la información de conexión necesaria para conectarse a Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e241-134">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1e241-135">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1e241-135">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="1e241-136">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e241-136">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1e241-137">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que ha creado, por ejemplo, **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="1e241-137">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="1e241-138">Haga clic en el nombre del servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="1e241-138">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="1e241-139">Seleccione la página **Introducción** del servidor.</span><span class="sxs-lookup"><span data-stu-id="1e241-139">Select the server's **Overview** page.</span></span> <span data-ttu-id="1e241-140">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="1e241-140">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="1e241-141">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="1e241-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="1e241-142">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="1e241-142">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="1e241-143">Conexión y creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="1e241-143">Connect and create a table</span></span>
<span data-ttu-id="1e241-144">Use el código siguiente para conectarse y crear una tabla mediante la instrucción SQL **CREATE TABLE**, seguida de las instrucciones SQL **INSERT INTO** para agregar filas a la tabla.</span><span class="sxs-lookup"><span data-stu-id="1e241-144">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="1e241-145">El código llama al método [pg_connect()](http://php.net/manual/en/function.pg-connect.php) para conectar con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e241-145">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1e241-146">A continuación, llama al método [pg_query()](http://php.net/manual/en/function.pg-query.php) varias veces para ejecutar varios comandos y a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) para consultar los detalles si se produjo un error cada vez.</span><span class="sxs-lookup"><span data-stu-id="1e241-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times to run several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred each time.</span></span> <span data-ttu-id="1e241-147">A continuación, llama al método [pg_close()](http://php.net/manual/en/function.pg-close.php) para cerrar la conexión.</span><span class="sxs-lookup"><span data-stu-id="1e241-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="1e241-148">Reemplace los parámetros `$host`, `$database`, `$user` y `$password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="1e241-148">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed to create connection to database: ". pg_last_error(). "<br/>");
    print "Successfully created connection to database.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a><span data-ttu-id="1e241-149">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="1e241-149">Read data</span></span>
<span data-ttu-id="1e241-150">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="1e241-150">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="1e241-151">El código llama al método [pg_connect()](http://php.net/manual/en/function.pg-connect.php) para conectar con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e241-151">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1e241-152">A continuación, llama al método [pg_query()](http://php.net/manual/en/function.pg-query.php) para ejecutar el comando SELECT (los resultados se guardan en un conjunto de resultados) y a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) para comprobar los detalles si se ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="1e241-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run the SELECT command, keeping the results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span>  <span data-ttu-id="1e241-153">Para leer el conjunto de resultados, se llama al método [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) en un bucle, una vez por cada fila, y los datos de la fila se recuperan en una matriz `$row`, con un valor de datos por columna en cada posición de dicha matriz.</span><span class="sxs-lookup"><span data-stu-id="1e241-153">To read the result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and the row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="1e241-154">Para liberar el conjunto de resultados, se llama al método [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php).</span><span class="sxs-lookup"><span data-stu-id="1e241-154">To free the result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="1e241-155">A continuación, llama al método [pg_close()](http://php.net/manual/en/function.pg-close.php) para cerrar la conexión.</span><span class="sxs-lookup"><span data-stu-id="1e241-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="1e241-156">Reemplace los parámetros `$host`, `$database`, `$user` y `$password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="1e241-156">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). "<br/>");

    print "Successfully created connection to database. <br/>";

    // Perform some SQL queries over the connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a><span data-ttu-id="1e241-157">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="1e241-157">Update data</span></span>
<span data-ttu-id="1e241-158">Use el código siguiente para conectarse y actualizar los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="1e241-158">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="1e241-159">El código llama al método [pg_connect()](http://php.net/manual/en/function.pg-connect.php) para conectar con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e241-159">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1e241-160">A continuación, llama al método [pg_query()](http://php.net/manual/en/function.pg-query.php) para ejecutar un comando, y a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) para comprobar los detalles si se ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="1e241-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="1e241-161">A continuación, llama al método [pg_close()](http://php.net/manual/en/function.pg-close.php) para cerrar la conexión.</span><span class="sxs-lookup"><span data-stu-id="1e241-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="1e241-162">Reemplace los parámetros `$host`, `$database`, `$user` y `$password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="1e241-162">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). ".<br/>");

    print "Successfully created connection to database. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a><span data-ttu-id="1e241-163">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="1e241-163">Delete data</span></span>
<span data-ttu-id="1e241-164">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="1e241-164">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="1e241-165">El código llama al método [pg_connect()](http://php.net/manual/en/function.pg-connect.php) para conectar con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e241-165">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to  Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1e241-166">A continuación, llama al método [pg_query()](http://php.net/manual/en/function.pg-query.php) para ejecutar un comando, y a [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) para comprobar los detalles si se ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="1e241-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="1e241-167">A continuación, llama al método [pg_close()](http://php.net/manual/en/function.pg-close.php) para cerrar la conexión.</span><span class="sxs-lookup"><span data-stu-id="1e241-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="1e241-168">Reemplace los parámetros `$host`, `$database`, `$user` y `$password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="1e241-168">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed to create connection to database: ". pg_last_error(). ". </br>");

    print "Successfully created connection to database. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a><span data-ttu-id="1e241-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e241-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1e241-170">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="1e241-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
