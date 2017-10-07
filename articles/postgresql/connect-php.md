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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Base de datos de Azure para PostgreSQL: Use PHP tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure base de datos PostgreSQL utilizando un [PHP](http://php.net/manual/intro-whatis.php) aplicación. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. En este artículo se da por supuesto que está familiarizado con el desarrollo con PHP, pero que se tooworking nueva con la base de datos de Azure para PostgreSQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Creación de la base de datos: Azure Portal](quickstart-create-server-database-portal.md)
- [Creación de la base de datos: CLI de Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Instalación de PHP
Instale PHP en su propio servidor o cree una [aplicación web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) de Azure que lo incluya.

### <a name="windows"></a>Windows
- Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://windows.php.net/download#php-7.1).
- Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.windows.php) para una configuración adicional
- código de Hello usa hello **pgsql** clase (ext/php_pgsql.dll) que se incluye en la instalación de PHP Hola. 
- Hola habilitado **pgsql** extensión editando el archivo de configuración php.ini hello, normalmente se encuentra en `C:\Program Files\PHP\v7.1\php.ini`. archivo de configuración de Hello debe contener una línea con el texto hello `extension=php_pgsql.so`. Si no está visible, agregue texto hello y guarde el archivo hello. Si el texto hello está presente, pero convertido en comentario con un prefijo de punto y coma, quite los comentarios texto hello mediante la eliminación de punto y coma de Hola.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://php.net/downloads.php). 
- Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.unix.php) para una configuración adicional
- código de Hello usa hello **pgsql** (php_pgsql.so) de la clase. Instálela mediante la ejecución de `sudo apt-get install php-pgsql`.
- Hola habilitado **pgsql** extensión mediante la edición de hello `/etc/php/7.0/mods-available/pgsql.ini` archivo de configuración. archivo de configuración de Hello debe contener una línea con el texto hello `extension=php_pgsql.so`. Si no está visible, agregue texto hello y guarde el archivo hello. Si el texto hello está presente, pero convertido en comentario con un prefijo de punto y coma, quite los comentarios texto hello mediante la eliminación de punto y coma de Hola.

### <a name="macos"></a>MacOS
- Descargue la [versión 7.1.4 de PHP](http://php.net/downloads.php).
- Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.macosx.php) para una configuración adicional

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.
3. Haga clic en el nombre del servidor de hello **mypgserver 20170401**.
4. Servidor de hello seleccione **Introducción** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-php/1-connection-string.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="connect-and-create-a-table"></a>Conexión y creación de una tabla
Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL, seguido de **INSERT INTO** tooadd filas de las instrucciones de SQL en la tabla de Hola.

método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de datos de PostgreSQL. A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun varias veces varios comandos y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si cada vez que se produjo un error. A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.

Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores. 

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

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. 

 método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de datos de PostgreSQL. A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun Hola del comando SELECT, mantener Hola de resultados en un conjunto de resultados y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si se produjo un error.  conjunto de resultados de tooread hello, método [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) se llama en un bucle, una vez por cada fila de Hola y de fila se recuperan los datos en una matriz `$row`, con el valor de datos por cada columna en cada posición de la matriz.  conjunto de resultados de toofree hello, método [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) se llama. A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.

Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores. 

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

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.

método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de datos de PostgreSQL. A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si se produjo un error. A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.

Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores. 

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


## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. 

 método de llamada de código de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect demasiado Azure base de datos de PostgreSQL. A continuación, llama el método [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, y [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck Hola detalla si se produjo un error. A continuación, llama el método [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose conexión de Hola.

Reemplace hello `$host`, `$database`, `$user`, y `$password` parámetros con sus propios valores. 

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

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./howto-migrate-using-export-and-import.md)
