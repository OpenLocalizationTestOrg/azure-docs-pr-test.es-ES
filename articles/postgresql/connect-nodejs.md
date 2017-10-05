---
title: "Conexión a Azure Database for PostgreSQL desde Node.js | Microsoft Docs"
description: "En este tutorial rápido se proporciona un ejemplo de código de Node.js que puede usar para conectarse y consultar datos desde Azure Database for PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: f6c98833c73b70bcf1f8ca53596a34f09807b276
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="3ca34-103">Azure Database for PostgreSQL: uso de Node.js para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="3ca34-103">Azure Database for PostgreSQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="3ca34-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for PostgreSQL mediante [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="3ca34-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="3ca34-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3ca34-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="3ca34-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante Node.js, pero que nunca ha trabajado con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ca34-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3ca34-107">Prerequisites</span></span>
<span data-ttu-id="3ca34-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="3ca34-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="3ca34-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3ca34-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="3ca34-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="3ca34-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="3ca34-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="3ca34-111">You also need to:</span></span>
- <span data-ttu-id="3ca34-112">Instalar [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="3ca34-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="3ca34-113">Instalación del cliente pg</span><span class="sxs-lookup"><span data-stu-id="3ca34-113">Install pg client</span></span>
<span data-ttu-id="3ca34-114">Instale [pg](https://www.npmjs.com/package/pg), que es un cliente de PostgreSQL para Node.js.</span><span class="sxs-lookup"><span data-stu-id="3ca34-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="3ca34-115">Para ello, ejecute el Administrador de paquetes de Node (npm) para JavaScript desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="3ca34-115">To do so, run the node package manager (npm) for JavaScript from your command line to install the pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="3ca34-116">Compruebe la instalación; para ello, enumere los paquetes instalados.</span><span class="sxs-lookup"><span data-stu-id="3ca34-116">Verify the installation by listing the packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="3ca34-117">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="3ca34-117">Get connection information</span></span>
<span data-ttu-id="3ca34-118">Obtenga la información de conexión necesaria para conectarse a Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-118">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="3ca34-119">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3ca34-119">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3ca34-120">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3ca34-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3ca34-121">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="3ca34-121">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created.</span></span>
3. <span data-ttu-id="3ca34-122">Haga clic en el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="3ca34-122">Click the server name.</span></span>
4. <span data-ttu-id="3ca34-123">Seleccione la página **Introducción** del servidor.</span><span class="sxs-lookup"><span data-stu-id="3ca34-123">Select the server's **Overview** page.</span></span> <span data-ttu-id="3ca34-124">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="3ca34-124">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3ca34-125">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="3ca34-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="3ca34-126">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="3ca34-126">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="3ca34-127">Ejecución del código de JavaScript en Node.js</span><span class="sxs-lookup"><span data-stu-id="3ca34-127">Running the JavaScript code in Node.js</span></span>
<span data-ttu-id="3ca34-128">Puede iniciar Node.js desde el shell de Bash o el símbolo del sistema de Windows; para ello, escriba `node` y luego copie y pegue el ejemplo de código de JavaScript para ejecutarlo de manera interactiva.</span><span class="sxs-lookup"><span data-stu-id="3ca34-128">You may launch Node.js from the bash shell or windows command prompt by typing `node`, then run the example JavaScript code interactively by copy and pasting it onto the prompt.</span></span> <span data-ttu-id="3ca34-129">También puede guardar el código de JavaScript en un archivo de texto e iniciar `node filename.js` con el nombre de archivo como parámetro para ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="3ca34-129">Alternatively, you may save the JavaScript code into a text file and launch `node filename.js` with the file name as a parameter to run it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="3ca34-130">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="3ca34-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="3ca34-131">Use el código siguiente para conectarse y cargar los datos mediante las instrucciones SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="3ca34-131">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="3ca34-132">El objeto [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) se usa para interactuar con el servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-132">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="3ca34-133">La función [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="3ca34-133">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="3ca34-134">La función [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) se usa para ejecutar la consulta SQL en la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-134">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="3ca34-135">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3ca34-135">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a><span data-ttu-id="3ca34-136">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="3ca34-136">Read data</span></span>
<span data-ttu-id="3ca34-137">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="3ca34-137">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="3ca34-138">El objeto [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) se usa para interactuar con el servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-138">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="3ca34-139">La función [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="3ca34-139">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="3ca34-140">La función [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) se usa para ejecutar la consulta SQL en la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-140">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="3ca34-141">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3ca34-141">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query to PostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a><span data-ttu-id="3ca34-142">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="3ca34-142">Update data</span></span>
<span data-ttu-id="3ca34-143">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="3ca34-143">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="3ca34-144">El objeto [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) se usa para interactuar con el servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-144">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="3ca34-145">La función [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="3ca34-145">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="3ca34-146">La función [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) se usa para ejecutar la consulta SQL en la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-146">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="3ca34-147">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3ca34-147">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a><span data-ttu-id="3ca34-148">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="3ca34-148">Delete data</span></span>
<span data-ttu-id="3ca34-149">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="3ca34-149">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="3ca34-150">El objeto [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) se usa para interactuar con el servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-150">The [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used to interface with the PostgreSQL server.</span></span> <span data-ttu-id="3ca34-151">La función [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) se usa para establecer la conexión al servidor.</span><span class="sxs-lookup"><span data-stu-id="3ca34-151">The [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used to establish the connection to the server.</span></span> <span data-ttu-id="3ca34-152">La función [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) se usa para ejecutar la consulta SQL en la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3ca34-152">The [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used to execute the SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="3ca34-153">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3ca34-153">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a><span data-ttu-id="3ca34-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ca34-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3ca34-155">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="3ca34-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
