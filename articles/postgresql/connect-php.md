---
title: aaaConnect tooAzure base de datos de PostgreSQL con PHP | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo de código PHP, puede usar tooconnect y consultar los datos de la base de datos PostgreSQL."
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
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="fe548-103">Base de datos de Azure para PostgreSQL: Use PHP tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="fe548-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="fe548-104">Este tutorial rápido muestra cómo tooconnect tooan Azure base de datos PostgreSQL utilizando un [PHP](http://php.net/manual/intro-whatis.php) aplicación.</span><span class="sxs-lookup"><span data-stu-id="fe548-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="fe548-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="fe548-106">En este artículo se da por supuesto que está familiarizado con el desarrollo con PHP, pero que se tooworking nueva con la base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe548-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fe548-107">Prerequisites</span></span>
<span data-ttu-id="fe548-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="fe548-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="fe548-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fe548-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="fe548-110">Creación de la base de datos: CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fe548-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="fe548-111">Instalación de PHP</span><span class="sxs-lookup"><span data-stu-id="fe548-111">Install PHP</span></span>
<span data-ttu-id="fe548-112">Instale PHP en su propio servidor o cree una [aplicación web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) de Azure que lo incluya.</span><span class="sxs-lookup"><span data-stu-id="fe548-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="fe548-113">Windows</span><span class="sxs-lookup"><span data-stu-id="fe548-113">Windows</span></span>
- <span data-ttu-id="fe548-114">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="fe548-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="fe548-115">Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.windows.php) para una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="fe548-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="fe548-116">código de Hello usa hello **pgsql** clase (ext/php_pgsql.dll) que se incluye en la instalación de PHP Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="fe548-117">Hola habilitado **pgsql** extensión editando el archivo de configuración php.ini hello, normalmente se encuentra en `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="fe548-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="fe548-118">archivo de configuración de Hello debe contener una línea con el texto hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="fe548-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="fe548-119">Si no está visible, agregue texto hello y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="fe548-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="fe548-120">Si el texto hello está presente, pero convertido en comentario con un prefijo de punto y coma, quite los comentarios texto hello mediante la eliminación de punto y coma de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="fe548-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="fe548-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="fe548-122">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="fe548-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="fe548-123">Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.unix.php) para una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="fe548-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="fe548-124">código de Hello usa hello **pgsql** (php_pgsql.so) de la clase.</span><span class="sxs-lookup"><span data-stu-id="fe548-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="fe548-125">Instálela mediante la ejecución de `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="fe548-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="fe548-126">Hola habilitado **pgsql** extensión mediante la edición de hello `/etc/php/7.0/mods-available/pgsql.ini` archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="fe548-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="fe548-127">archivo de configuración de Hello debe contener una línea con el texto hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="fe548-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="fe548-128">Si no está visible, agregue texto hello y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="fe548-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="fe548-129">Si el texto hello está presente, pero convertido en comentario con un prefijo de punto y coma, quite los comentarios texto hello mediante la eliminación de punto y coma de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="fe548-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="fe548-130">MacOS</span></span>
- <span data-ttu-id="fe548-131">Descargue la [versión 7.1.4 de PHP](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="fe548-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="fe548-132">Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.macosx.php) para una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="fe548-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="fe548-133">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="fe548-133">Get connection information</span></span>
<span data-ttu-id="fe548-134">Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="fe548-135">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="fe548-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="fe548-136">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fe548-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fe548-137">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="fe548-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="fe548-138">Haga clic en el nombre del servidor de hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="fe548-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="fe548-139">Servidor de hello seleccione **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="fe548-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="fe548-140">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="fe548-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="fe548-141">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="fe548-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="fe548-142">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="fe548-143">Conexión y creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="fe548-143">Connect and create a table</span></span>
<span data-ttu-id="fe548-144">Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL, seguido de **INSERT INTO** tooadd filas de las instrucciones de SQL en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="fe548-145">método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="fe548-146">A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun varias veces varios comandos y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si cada vez que se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="fe548-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="fe548-147">A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="fe548-148">Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="fe548-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

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

## <a name="read-data"></a><span data-ttu-id="fe548-149">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="fe548-149">Read data</span></span>
<span data-ttu-id="fe548-150">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="fe548-151">método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="fe548-152">A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun Hola del comando SELECT, mantener Hola de resultados en un conjunto de resultados y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="fe548-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="fe548-153">conjunto de resultados de tooread hello, método [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) se llama en un bucle, una vez por cada fila de Hola y de fila se recuperan los datos en una matriz `$row`, con el valor de datos por cada columna en cada posición de la matriz.</span><span class="sxs-lookup"><span data-stu-id="fe548-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="fe548-154">conjunto de resultados de toofree hello, método [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) se llama.</span><span class="sxs-lookup"><span data-stu-id="fe548-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="fe548-155">A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="fe548-156">Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="fe548-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
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

## <a name="update-data"></a><span data-ttu-id="fe548-157">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="fe548-157">Update data</span></span>
<span data-ttu-id="fe548-158">Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="fe548-159">método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="fe548-160">A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="fe548-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="fe548-161">A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="fe548-162">Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="fe548-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

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


## <a name="delete-data"></a><span data-ttu-id="fe548-163">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="fe548-163">Delete data</span></span>
<span data-ttu-id="fe548-164">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="fe548-165">método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect demasiado Azure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fe548-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="fe548-166">A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="fe548-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="fe548-167">A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe548-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="fe548-168">Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="fe548-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

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

## <a name="next-steps"></a><span data-ttu-id="fe548-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe548-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fe548-170">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="fe548-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
