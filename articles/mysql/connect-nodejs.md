---
title: "Conexión a Azure Database for MySQL desde Node.js | Microsoft Docs"
description: "En este tutorial rápido se proporcionan ejemplos de código Node.js que se pueden usar para conectarse a Azure Database for MySQL y consultar datos en este servicio."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: 0c0bd4b707c114d2991e5f0473a4bfbe9e463e3c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="846a0-103">Azure Database for MySQL: uso de Node.js para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="846a0-103">Azure Database for MySQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="846a0-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for MySQL mediante [Node.js](https://nodejs.org/) desde las plataformas Windows, Ubuntu Linux y Mac.</span><span class="sxs-lookup"><span data-stu-id="846a0-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="846a0-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="846a0-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="846a0-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante Node.js, pero que nunca ha trabajado con Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="846a0-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="846a0-107">Prerequisites</span></span>
<span data-ttu-id="846a0-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="846a0-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="846a0-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="846a0-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="846a0-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="846a0-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="846a0-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="846a0-111">You also need to:</span></span>
- <span data-ttu-id="846a0-112">Instalar el entorno de tiempo de ejecución de [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="846a0-112">Install the [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="846a0-113">Instalar el paquete [mysql2](https://www.npmjs.com/package/mysql2) para conectarse a MySQL desde la aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="846a0-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span></span> 

## <a name="install-nodejs-and-the-mysql-connector"></a><span data-ttu-id="846a0-114">Instalación de Node.js y el conector de MySQL</span><span class="sxs-lookup"><span data-stu-id="846a0-114">Install Node.js and the MySQL connector</span></span>
<span data-ttu-id="846a0-115">Dependiendo de la plataforma, siga las instrucciones apropiadas para instalar Node.js.</span><span class="sxs-lookup"><span data-stu-id="846a0-115">Depending on your platform, follow the appropriate instructions to install Node.js.</span></span> <span data-ttu-id="846a0-116">Use npm para instalar el paquete de mysql2 y sus dependencias en la carpeta de proyecto.</span><span class="sxs-lookup"><span data-stu-id="846a0-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="846a0-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="846a0-117">**Windows**</span></span>
1. <span data-ttu-id="846a0-118">Visite la [página de descargas de Node.js](https://nodejs.org/en/download/) y seleccione la opción deseada de Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="846a0-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="846a0-119">Cree una carpeta de proyecto local, como `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="846a0-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="846a0-120">Inicie el símbolo del sistema y cambie el directorio a la carpeta de proyecto, por ejemplo, `cd c:\nodejsmysql\`.</span><span class="sxs-lookup"><span data-stu-id="846a0-120">Launch the command prompt and cd into the project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="846a0-121">Ejecute la herramienta NPM para instalar la biblioteca de mysql2 en la carpeta de proyecto.</span><span class="sxs-lookup"><span data-stu-id="846a0-121">Run the NPM tool to install the mysql2 library into the project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="846a0-122">Para comprobar la instalación, examine el texto de salida de `npm list` para `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="846a0-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="846a0-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="846a0-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="846a0-124">Ejecute los siguientes comandos para instalar **Node.js** y **npm**, el Administrador de paquetes para Node.js.</span><span class="sxs-lookup"><span data-stu-id="846a0-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="846a0-125">Ejecute los comandos siguientes para crear una carpeta de proyecto `mysqlnodejs` e instale el paquete mysql2 en ella.</span><span class="sxs-lookup"><span data-stu-id="846a0-125">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="846a0-126">Para comprobar la instalación, examine el texto de salida de npm list para `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="846a0-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="846a0-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="846a0-127">**Mac OS**</span></span>
1. <span data-ttu-id="846a0-128">Escriba los comandos siguientes para instalar **brew**, un administrador de paquetes fácil de usar para Mac OS X y **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="846a0-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="846a0-129">Ejecute los comandos siguientes para crear una carpeta de proyecto `mysqlnodejs` e instale el paquete mysql2 en ella.</span><span class="sxs-lookup"><span data-stu-id="846a0-129">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="846a0-130">Para comprobar la instalación, examine el texto de salida de `npm list` para `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="846a0-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="846a0-131">El número de versión puede variar a medida que se publiquen nuevas revisiones.</span><span class="sxs-lookup"><span data-stu-id="846a0-131">The version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="846a0-132">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="846a0-132">Get connection information</span></span>
<span data-ttu-id="846a0-133">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="846a0-134">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="846a0-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="846a0-135">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="846a0-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="846a0-136">En el panel izquierdo, haga clic en **Todos los recursos** y, a continuación, busque el servidor que ha creado (por ejemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="846a0-136">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="846a0-137">Haga clic en el nombre del servidor **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="846a0-137">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="846a0-138">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="846a0-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="846a0-139">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="846a0-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="846a0-140">![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="846a0-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="846a0-141">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="846a0-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="846a0-142">Ejecución del código de JavaScript en Node.js</span><span class="sxs-lookup"><span data-stu-id="846a0-142">Running the JavaScript code in Node.js</span></span>
1. <span data-ttu-id="846a0-143">Pegue el código de JavaScript en archivos de texto y guárdelos en una carpeta de proyecto con la extensión .js, por ejemplo, C:\nodejsmysql\createtable.js o /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="846a0-143">Paste the JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="846a0-144">Inicie el símbolo del sistema o el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="846a0-144">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="846a0-145">Cambie el directorio a la carpeta de proyecto `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="846a0-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="846a0-146">Para ejecutar la aplicación, escriba el comando node seguido del nombre de archivo, por ejemplo, `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="846a0-146">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="846a0-147">En Windows, si la aplicación de Node no está en la ruta de la variable de entorno, puede que deba usar la ruta de acceso completa para iniciar la aplicación de Node, por ejemplo, `"C:\Program Files\nodejs\node.exe" createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="846a0-147">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="846a0-148">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="846a0-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="846a0-149">Use el código siguiente para conectarse y cargar los datos mediante las instrucciones SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="846a0-149">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="846a0-150">El método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) se usa para interactuar con el servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-150">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="846a0-151">La función [connect()](https://github.com/mysqljs/mysql#establishing-connections) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="846a0-151">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span></span> <span data-ttu-id="846a0-152">La función [query()](https://github.com/mysqljs/mysql#performing-queries) se usa para ejecutar la consulta SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-152">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="846a0-153">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="846a0-153">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="846a0-154">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="846a0-154">Read data</span></span>
<span data-ttu-id="846a0-155">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="846a0-155">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="846a0-156">El método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) se usa para interactuar con el servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-156">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="846a0-157">El método [connect()](https://github.com/mysqljs/mysql#establishing-connections) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="846a0-157">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="846a0-158">El método [query()](https://github.com/mysqljs/mysql#performing-queries) se usa para ejecutar la consulta SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-158">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> <span data-ttu-id="846a0-159">La matriz de resultados se usa para almacenar los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="846a0-159">The results array is used to hold the results of the query.</span></span>

<span data-ttu-id="846a0-160">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="846a0-160">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="846a0-161">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="846a0-161">Update data</span></span>
<span data-ttu-id="846a0-162">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="846a0-162">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="846a0-163">El método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) se usa para interactuar con el servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-163">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="846a0-164">El método [connect()](https://github.com/mysqljs/mysql#establishing-connections) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="846a0-164">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="846a0-165">El método [query()](https://github.com/mysqljs/mysql#performing-queries) se usa para ejecutar la consulta SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-165">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="846a0-166">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="846a0-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="846a0-167">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="846a0-167">Delete data</span></span>
<span data-ttu-id="846a0-168">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="846a0-168">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="846a0-169">El método [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) se usa para interactuar con el servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-169">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="846a0-170">El método [connect()](https://github.com/mysqljs/mysql#establishing-connections) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="846a0-170">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="846a0-171">El método [query()](https://github.com/mysqljs/mysql#performing-queries) se usa para ejecutar la consulta SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="846a0-171">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="846a0-172">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="846a0-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="846a0-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="846a0-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="846a0-174">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="846a0-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
