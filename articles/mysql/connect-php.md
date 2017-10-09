---
title: Conectar tooAzure base de datos de MySQL desde PHP | Documentos de Microsoft
description: "Este tutorial rápido proporciona varios ejemplos de código PHP puede usar tooconnect y consultar los datos de la base de datos MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Base de datos de Azure para MySQL: Use PHP tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos de MySQL utilizando un [PHP](http://php.net/manual/intro-whatis.php) aplicación. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. En este artículo se da por supuesto que está familiarizado con el desarrollo con PHP, pero que se tooworking nueva con la base de datos de Azure para MySQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

## <a name="install-php"></a>Instalación de PHP
Instale PHP en su propio servidor o cree una [aplicación web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) de Azure que lo incluya.

### <a name="macos"></a>MacOS
- Descargue la [versión 7.1.4 de PHP](http://php.net/downloads.php).
- Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.macosx.php) para una configuración adicional

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://php.net/downloads.php).
- Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.unix.php) para una configuración adicional

### <a name="windows"></a>Windows
- Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://windows.php.net/download#php-7.1).
- Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.windows.php) para una configuración adicional

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el panel izquierdo de hello, haga clic en **todos los recursos**y, a continuación, busque servidor Hola se haya creado (por ejemplo, **myserver4demo**).
3. Haga clic en el nombre del servidor de Hola.
4. Servidor de hello seleccione **propiedades** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Nombre del servidor de Azure Database for MySQL](./media/connect-php/1_server-properties-name-login.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="connect-and-create-a-table"></a>Conexión y creación de una tabla
Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL. 

código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP. Hola llamar a métodos de código [mysqli_init](http://php.net/manual/mysqli.init.php) y [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. A continuación, llama el método [mysqli_query](http://php.net/manual/mysqli.query.php) toorun consulta de Hola. A continuación, llama el método [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose conexión de Hola.

Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Insertar datos
Código tooconnect siguiente de Hola de uso e insertar datos mediante un **insertar** instrucción SQL.

código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP. código de Hello usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate preparación de una instrucción insert, a continuación, enlaza Hola parámetros para cada valor de columna insertada mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). instrucción hello mediante el método ejecuta el código de Hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después se cierra Hola instrucción mediante el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.  código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP. código de Hello usa el método [mysqli_query](http://php.net/manual/mysqli.query.php) realizar consultas de sql de Hola y usa [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) método toofetch Hola filas resultantes.

Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.

código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP. código de Hello usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate una instrucción update preparada, a continuación, enlaza los parámetros de Hola para cada valor de las filas actualizadas mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). instrucción hello mediante el método ejecuta el código de Hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después se cierra Hola instrucción mediante el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. 

código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP. código de Hello usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate preparación de una instrucción delete, a continuación, enlaza Hola parámetros para Hola donde cláusula de instrucción de hello mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). instrucción hello mediante el método ejecuta el código de Hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después se cierra Hola instrucción mediante el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Compilación de una aplicación web PHP y MySQL en Azure](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
