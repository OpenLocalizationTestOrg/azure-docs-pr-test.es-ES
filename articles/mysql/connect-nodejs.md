---
title: Conectar tooAzure base de datos de MySQL de Node.js | Documentos de Microsoft
description: "Este tutorial rápido proporciona varios ejemplos de código de Node.js puede usar tooconnect y consultar los datos de la base de datos MySQL."
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
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="3c3c4-103">Base de datos de Azure para MySQL: Use Node.js tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="3c3c4-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="3c3c4-104">Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos para el uso de MySQL [Node.js](https://nodejs.org/) entre plataformas de Windows, Ubuntu Linux y Mac.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="3c3c4-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="3c3c4-106">Hello pasos descritos en este artículo suponen que está familiarizado con el desarrollo utilizando Node.js, y que tooworking nueva con la base de datos de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c3c4-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3c3c4-107">Prerequisites</span></span>
<span data-ttu-id="3c3c4-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="3c3c4-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="3c3c4-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="3c3c4-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="3c3c4-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="3c3c4-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="3c3c4-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="3c3c4-111">You also need to:</span></span>
- <span data-ttu-id="3c3c4-112">Instalar hello [Node.js](https://nodejs.org) en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="3c3c4-113">Instalar [mysql2](https://www.npmjs.com/package/mysql2) tooconnect tooMySQL de hello aplicación Node.js del paquete.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="3c3c4-114">Instalar Node.js y Hola conector MySQL</span><span class="sxs-lookup"><span data-stu-id="3c3c4-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="3c3c4-115">Dependiendo de la plataforma, siga Hola instrucciones apropiadas tooinstall Node.js.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="3c3c4-116">Usar npm tooinstall hello mysql2 paquete y sus dependencias en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="3c3c4-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="3c3c4-117">**Windows**</span></span>
1. <span data-ttu-id="3c3c4-118">Visite hello [página de descargas de Node.js](https://nodejs.org/en/download/) y seleccione la opción deseada del instalador de Windows.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="3c3c4-119">Cree una carpeta de proyecto local, como `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="3c3c4-120">Inicie símbolo hello y cd en la carpeta del proyecto hello, como`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="3c3c4-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="3c3c4-121">Ejecute biblioteca de hello NPM herramienta tooinstall hello mysql2 en la carpeta del proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="3c3c4-122">Comprobar instalación Hola Hola `npm list` salida de texto para `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="3c3c4-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="3c3c4-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="3c3c4-124">Siguiente ejecución Hola comandos tooinstall **Node.js** y **npm** Administrador de paquetes de saludo para Node.js.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="3c3c4-125">Ejecute hello después comandos toomake una carpeta de proyecto `mysqlnodejs` e instale el paquete de mysql2 de hello en esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="3c3c4-126">Comprobar la instalación de hello activando el texto de salida de la lista de npm para `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="3c3c4-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="3c3c4-127">**Mac OS**</span></span>
1. <span data-ttu-id="3c3c4-128">Escriba Hola después comandos tooinstall **brew**, un administrador de paquetes de fácil de usar para Mac OS X y **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="3c3c4-129">Ejecute hello después comandos toomake una carpeta de proyecto `mysqlnodejs` e instale el paquete de mysql2 de hello en esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="3c3c4-130">Comprobar instalación Hola Hola `npm list` salida de texto para `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="3c3c4-131">Hello número de versión puede variar a medida que se publiquen nuevas revisiones.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="3c3c4-132">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="3c3c4-132">Get connection information</span></span>
<span data-ttu-id="3c3c4-133">Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="3c3c4-134">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3c3c4-135">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c3c4-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3c3c4-136">En el panel izquierdo de hello, haga clic en **todos los recursos**y, a continuación, busque servidor Hola se haya creado (por ejemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="3c3c4-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="3c3c4-137">Haga clic en el nombre del servidor de hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="3c3c4-138">Servidor de hello seleccione **propiedades** página.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="3c3c4-139">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3c3c4-140">![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="3c3c4-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="3c3c4-141">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="3c3c4-142">Ejecutar código de JavaScript de hello en Node.js</span><span class="sxs-lookup"><span data-stu-id="3c3c4-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="3c3c4-143">Pegue el código de JavaScript de hello en archivos de texto y guarde en una carpeta del proyecto con .js de extensión de archivo, como C:\nodejsmysql\createtable.js o /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="3c3c4-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="3c3c4-144">Inicie el símbolo del sistema de Hola o el shell de bash.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="3c3c4-145">Cambie el directorio a la carpeta de proyecto `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="3c3c4-146">aplicación de hello toorun, escriba Hola nodo comando seguido por nombre de archivo de hello, como `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="3c3c4-147">En Windows, si la aplicación de nodo de hello no está en la ruta de la variable de entorno, puede necesita toouse Hola ruta de acceso completa toolaunch Hola nodo aplicación, como`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="3c3c4-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="3c3c4-148">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="3c3c4-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="3c3c4-149">Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="3c3c4-150">Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="3c3c4-151">Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) función es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="3c3c4-152">Hola [query()](https://github.com/mysqljs/mysql#performing-queries) función es consulta SQL hello tooexecute usado en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="3c3c4-153">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="3c3c4-154">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="3c3c4-154">Read data</span></span>
<span data-ttu-id="3c3c4-155">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="3c3c4-156">Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="3c3c4-157">Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) método es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="3c3c4-158">Hola [query()](https://github.com/mysqljs/mysql#performing-queries) método es consulta SQL hello tooexecute usado en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="3c3c4-159">matriz de resultados de Hello es toohold usado Hola resultados de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="3c3c4-160">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="3c3c4-161">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="3c3c4-161">Update data</span></span>
<span data-ttu-id="3c3c4-162">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="3c3c4-163">Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="3c3c4-164">Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) método es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="3c3c4-165">Hola [query()](https://github.com/mysqljs/mysql#performing-queries) método es consulta SQL hello tooexecute usado en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="3c3c4-166">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="3c3c4-167">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="3c3c4-167">Delete data</span></span>
<span data-ttu-id="3c3c4-168">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="3c3c4-169">Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="3c3c4-170">Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) método es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="3c3c4-171">Hola [query()](https://github.com/mysqljs/mysql#performing-queries) método es consulta SQL hello tooexecute usado en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="3c3c4-172">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3c3c4-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3c3c4-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c3c4-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3c3c4-174">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="3c3c4-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
