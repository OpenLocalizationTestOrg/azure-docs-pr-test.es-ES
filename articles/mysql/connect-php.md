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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="b6a66-103">Base de datos de Azure para MySQL: Use PHP tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="b6a66-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="b6a66-104">Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos de MySQL utilizando un [PHP](http://php.net/manual/intro-whatis.php) aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6a66-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="b6a66-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6a66-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="b6a66-106">En este artículo se da por supuesto que está familiarizado con el desarrollo con PHP, pero que se tooworking nueva con la base de datos de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6a66-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b6a66-107">Prerequisites</span></span>
<span data-ttu-id="b6a66-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="b6a66-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="b6a66-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="b6a66-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="b6a66-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="b6a66-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-php"></a><span data-ttu-id="b6a66-111">Instalación de PHP</span><span class="sxs-lookup"><span data-stu-id="b6a66-111">Install PHP</span></span>
<span data-ttu-id="b6a66-112">Instale PHP en su propio servidor o cree una [aplicación web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) de Azure que lo incluya.</span><span class="sxs-lookup"><span data-stu-id="b6a66-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="b6a66-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="b6a66-113">MacOS</span></span>
- <span data-ttu-id="b6a66-114">Descargue la [versión 7.1.4 de PHP](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="b6a66-115">Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.macosx.php) para una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="b6a66-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="b6a66-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b6a66-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="b6a66-117">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="b6a66-118">Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.unix.php) para una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="b6a66-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="b6a66-119">Windows</span><span class="sxs-lookup"><span data-stu-id="b6a66-119">Windows</span></span>
- <span data-ttu-id="b6a66-120">Descargue la [versión segura 7.1.4 de PHP sin subprocesos (x64)](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="b6a66-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="b6a66-121">Instalar PHP y consulte toohello [manual de PHP](http://php.net/manual/install.windows.php) para una configuración adicional</span><span class="sxs-lookup"><span data-stu-id="b6a66-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b6a66-122">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="b6a66-122">Get connection information</span></span>
<span data-ttu-id="b6a66-123">Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="b6a66-124">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="b6a66-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b6a66-125">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b6a66-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b6a66-126">En el panel izquierdo de hello, haga clic en **todos los recursos**y, a continuación, busque servidor Hola se haya creado (por ejemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="b6a66-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="b6a66-127">Haga clic en el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6a66-127">Click hello server name.</span></span>
4. <span data-ttu-id="b6a66-128">Servidor de hello seleccione **propiedades** página.</span><span class="sxs-lookup"><span data-stu-id="b6a66-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="b6a66-129">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="b6a66-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b6a66-130">![Nombre del servidor de Azure Database for MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b6a66-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b6a66-131">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6a66-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="b6a66-132">Conexión y creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="b6a66-132">Connect and create a table</span></span>
<span data-ttu-id="b6a66-133">Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="b6a66-134">código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP.</span><span class="sxs-lookup"><span data-stu-id="b6a66-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b6a66-135">Hola llamar a métodos de código [mysqli_init](http://php.net/manual/mysqli.init.php) y [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="b6a66-136">A continuación, llama el método [mysqli_query](http://php.net/manual/mysqli.query.php) toorun consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6a66-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="b6a66-137">A continuación, llama el método [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6a66-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="b6a66-138">Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="b6a66-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="insert-data"></a><span data-ttu-id="b6a66-139">Insertar datos</span><span class="sxs-lookup"><span data-stu-id="b6a66-139">Insert data</span></span>
<span data-ttu-id="b6a66-140">Código tooconnect siguiente de Hola de uso e insertar datos mediante un **insertar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="b6a66-141">código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP.</span><span class="sxs-lookup"><span data-stu-id="b6a66-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b6a66-142">código de Hello usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate preparación de una instrucción insert, a continuación, enlaza Hola parámetros para cada valor de columna insertada mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="b6a66-143">instrucción hello mediante el método ejecuta el código de Hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después se cierra Hola instrucción mediante el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="b6a66-144">Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="b6a66-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="b6a66-145">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="b6a66-145">Read data</span></span>
<span data-ttu-id="b6a66-146">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="b6a66-147">código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP.</span><span class="sxs-lookup"><span data-stu-id="b6a66-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b6a66-148">código de Hello usa el método [mysqli_query](http://php.net/manual/mysqli.query.php) realizar consultas de sql de Hola y usa [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) método toofetch Hola filas resultantes.</span><span class="sxs-lookup"><span data-stu-id="b6a66-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="b6a66-149">Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="b6a66-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="b6a66-150">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="b6a66-150">Update data</span></span>
<span data-ttu-id="b6a66-151">Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="b6a66-152">código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP.</span><span class="sxs-lookup"><span data-stu-id="b6a66-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b6a66-153">código de Hello usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate una instrucción update preparada, a continuación, enlaza los parámetros de Hola para cada valor de las filas actualizadas mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="b6a66-154">instrucción hello mediante el método ejecuta el código de Hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después se cierra Hola instrucción mediante el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="b6a66-155">Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="b6a66-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="b6a66-156">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="b6a66-156">Delete data</span></span>
<span data-ttu-id="b6a66-157">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="b6a66-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="b6a66-158">código de Hello usa hello **extensión MySQL mejorado** clase (mysqli) incluido en PHP.</span><span class="sxs-lookup"><span data-stu-id="b6a66-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b6a66-159">código de Hello usa el método [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate preparación de una instrucción delete, a continuación, enlaza Hola parámetros para Hola donde cláusula de instrucción de hello mediante el método [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="b6a66-160">instrucción hello mediante el método ejecuta el código de Hello [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) y después se cierra Hola instrucción mediante el método [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="b6a66-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="b6a66-161">Reemplazar parámetros de host, nombre de usuario, contraseña y db_name de hello con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="b6a66-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="b6a66-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6a66-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b6a66-163">Compilación de una aplicación web PHP y MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="b6a66-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
