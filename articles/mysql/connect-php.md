---
title: "Conexión a Azure Database for MySQL desde PHP | Microsoft Docs"
description: "En este tutorial rápido se proporcionan ejemplos de código de PHP que se pueden usar para conectarse a Azure Database for MySQL y consultar datos en este servicio."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 59da1ab9e76685d7ed0c4415ef99578c982e956c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a><span data-ttu-id="cf320-103">Azure Database for MySQL: uso de PHP para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="cf320-103">Azure Database for MySQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="cf320-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for MySQL mediante una aplicación de [PHP](http://php.net/manual/intro-whatis.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="cf320-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="cf320-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="cf320-106">En este artículo se da por hecho que está familiarizado con el desarrollo mediante PHP, pero que nunca ha usado Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="cf320-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf320-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cf320-107">Prerequisites</span></span>
<span data-ttu-id="cf320-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="cf320-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="cf320-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="cf320-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="cf320-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="cf320-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-php"></a><span data-ttu-id="cf320-111">Instalación de PHP</span><span class="sxs-lookup"><span data-stu-id="cf320-111">Install PHP</span></span>
<span data-ttu-id="cf320-112">Instale PHP en su propio servidor o cree una [aplicación web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) de Azure que lo incluya.</span><span class="sxs-lookup"><span data-stu-id="cf320-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="cf320-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="cf320-113">MacOS</span></span>
- <span data-ttu-id="cf320-114">Descargue la [versión 7.1.4 de PHP](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="cf320-115">Instale PHP y consulte el [manual de PHP](http://php.net/manual/install.macosx.php) para continuar con la configuración.</span><span class="sxs-lookup"><span data-stu-id="cf320-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="cf320-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="cf320-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="cf320-117">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="cf320-118">Instale PHP y consulte el [manual de PHP](http://php.net/manual/install.unix.php) para continuar con la configuración.</span><span class="sxs-lookup"><span data-stu-id="cf320-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="cf320-119">Windows</span><span class="sxs-lookup"><span data-stu-id="cf320-119">Windows</span></span>
- <span data-ttu-id="cf320-120">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="cf320-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="cf320-121">Instale PHP y consulte el [manual de PHP](http://php.net/manual/install.windows.php) para continuar con la configuración.</span><span class="sxs-lookup"><span data-stu-id="cf320-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="cf320-122">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="cf320-122">Get connection information</span></span>
<span data-ttu-id="cf320-123">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="cf320-123">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="cf320-124">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="cf320-124">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="cf320-125">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf320-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf320-126">En el panel izquierdo, haga clic en **Todos los recursos** y, a continuación, busque el servidor que ha creado (por ejemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="cf320-126">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="cf320-127">Haga clic en el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="cf320-127">Click the server name.</span></span>
4. <span data-ttu-id="cf320-128">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="cf320-128">Select the server's **Properties** page.</span></span> <span data-ttu-id="cf320-129">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="cf320-129">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="cf320-130">![Nombre del servidor de Azure Database for MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="cf320-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="cf320-131">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="cf320-131">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="cf320-132">Conexión y creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="cf320-132">Connect and create a table</span></span>
<span data-ttu-id="cf320-133">Use el código siguiente para crear una tabla y conectarla mediante la instrucción SQL **CREATE TABLE**.</span><span class="sxs-lookup"><span data-stu-id="cf320-133">Use the following code to connect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="cf320-134">El código usa la clase **MySQL Improved extension** (mysqli) incluida en PHP.</span><span class="sxs-lookup"><span data-stu-id="cf320-134">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="cf320-135">El código realiza una llamada a los métodos [mysqli_init](http://php.net/manual/mysqli.init.php) y [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) para conectarse a MySQL.</span><span class="sxs-lookup"><span data-stu-id="cf320-135">The code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span></span> <span data-ttu-id="cf320-136">A continuación, llama al método [mysqli_query](http://php.net/manual/mysqli.query.php) para ejecutar la consulta.</span><span class="sxs-lookup"><span data-stu-id="cf320-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span></span> <span data-ttu-id="cf320-137">A continuación, llama al método [mysqli_close](http://php.net/manual/mysqli.close.php) para cerrar la conexión.</span><span class="sxs-lookup"><span data-stu-id="cf320-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span></span>

<span data-ttu-id="cf320-138">Reemplace los parámetros de host, username, password y db_name con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="cf320-138">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
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

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="cf320-139">Insertar datos</span><span class="sxs-lookup"><span data-stu-id="cf320-139">Insert data</span></span>
<span data-ttu-id="cf320-140">Use el código siguiente para conectarse e insertar datos mediante la instrucción SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="cf320-140">Use the following code to connect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="cf320-141">El código usa la clase **MySQL Improved extension** (mysqli) incluida en PHP.</span><span class="sxs-lookup"><span data-stu-id="cf320-141">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="cf320-142">El código usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) para crear una instrucción insert preparada y enlaza los parámetros para cada valor de columna insertado mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-142">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="cf320-143">El código ejecuta la instrucción con el método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después la cierra con el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-143">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="cf320-144">Reemplace los parámetros de host, username, password y db_name con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="cf320-144">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
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

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="cf320-145">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="cf320-145">Read data</span></span>
<span data-ttu-id="cf320-146">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="cf320-146">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="cf320-147">El código usa la clase **MySQL Improved extension** (mysqli) incluida en PHP.</span><span class="sxs-lookup"><span data-stu-id="cf320-147">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="cf320-148">El código usa el método [mysqli_query](http://php.net/manual/mysqli.query.php) para realizar la consulta sql y el método [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) para capturar las filas resultantes.</span><span class="sxs-lookup"><span data-stu-id="cf320-148">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method to fetch the resulting rows.</span></span>

<span data-ttu-id="cf320-149">Reemplace los parámetros de host, username, password y db_name con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="cf320-149">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="cf320-150">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="cf320-150">Update data</span></span>
<span data-ttu-id="cf320-151">Use el código siguiente para conectarse y actualizar los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="cf320-151">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="cf320-152">El código usa la clase **MySQL Improved extension** (mysqli) incluida en PHP.</span><span class="sxs-lookup"><span data-stu-id="cf320-152">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="cf320-153">El código usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) para crear una instrucción update preparada y enlaza los parámetros para cada valor de columna actualizado mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-153">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="cf320-154">El código ejecuta la instrucción con el método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después la cierra con el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-154">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="cf320-155">Reemplace los parámetros de host, username, password y db_name con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="cf320-155">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="cf320-156">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="cf320-156">Delete data</span></span>
<span data-ttu-id="cf320-157">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="cf320-157">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="cf320-158">El código usa la clase **MySQL Improved extension** (mysqli) incluida en PHP.</span><span class="sxs-lookup"><span data-stu-id="cf320-158">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="cf320-159">El código usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) para crear una instrucción delete preparada y enlaza los parámetros para la cláusula where de la instrucción mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-159">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="cf320-160">El código ejecuta la instrucción con el método [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después la cierra con el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="cf320-160">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="cf320-161">Reemplace los parámetros de host, username, password y db_name con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="cf320-161">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="cf320-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf320-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cf320-163">Compilación de una aplicación web PHP y MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="cf320-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
