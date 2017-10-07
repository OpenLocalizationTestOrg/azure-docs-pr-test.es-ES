---
title: Conectar tooAzure base de datos de PostgreSQL de Node.js | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo de código de Node.js puede usar tooconnect y consultar los datos de la base de datos PostgreSQL."
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
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="11f61-103">Base de datos de Azure para PostgreSQL: Use Node.js tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="11f61-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="11f61-104">Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos para el uso de PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="11f61-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="11f61-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f61-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="11f61-106">Hello pasos descritos en este artículo suponen que está familiarizado con el desarrollo utilizando Node.js, y que tooworking nueva con la base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11f61-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="11f61-107">Prerequisites</span></span>
<span data-ttu-id="11f61-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="11f61-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="11f61-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="11f61-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="11f61-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="11f61-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="11f61-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="11f61-111">You also need to:</span></span>
- <span data-ttu-id="11f61-112">Instalar [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="11f61-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="11f61-113">Instalación del cliente pg</span><span class="sxs-lookup"><span data-stu-id="11f61-113">Install pg client</span></span>
<span data-ttu-id="11f61-114">Instale [pg](https://www.npmjs.com/package/pg), que es un cliente de PostgreSQL para Node.js.</span><span class="sxs-lookup"><span data-stu-id="11f61-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="11f61-115">por lo tanto, los toodo ejecutar Administrador de paquetes de nodo de hello (npm) para JavaScript desde el cliente de línea de comandos tooinstall Hola pg.</span><span class="sxs-lookup"><span data-stu-id="11f61-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="11f61-116">Comprobar la instalación de hello listado de paquetes de saludo instalados.</span><span class="sxs-lookup"><span data-stu-id="11f61-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="11f61-117">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="11f61-117">Get connection information</span></span>
<span data-ttu-id="11f61-118">Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="11f61-119">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="11f61-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="11f61-120">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="11f61-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="11f61-121">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="11f61-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="11f61-122">Haga clic en el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f61-122">Click hello server name.</span></span>
4. <span data-ttu-id="11f61-123">Servidor de hello seleccione **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="11f61-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="11f61-124">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="11f61-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="11f61-125">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="11f61-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="11f61-126">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f61-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="11f61-127">Ejecutar código de JavaScript de hello en Node.js</span><span class="sxs-lookup"><span data-stu-id="11f61-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="11f61-128">Puede iniciar Node.js Hola intensiva de shell o windows desde línea de comandos escribiendo `node`, a continuación, ejecutar código de JavaScript de ejemplo de Hola de forma interactiva mediante copia y pegar en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f61-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="11f61-129">Como alternativa, puede guardar código de JavaScript de hello en un archivo de texto e inicie `node filename.js` con el nombre de archivo de Hola como un parámetro toorun.</span><span class="sxs-lookup"><span data-stu-id="11f61-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="11f61-130">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="11f61-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="11f61-131">Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="11f61-132">Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="11f61-133">Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="11f61-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="11f61-134">Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="11f61-135">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="11f61-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="11f61-136">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="11f61-136">Read data</span></span>
<span data-ttu-id="11f61-137">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="11f61-138">Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="11f61-139">Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="11f61-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="11f61-140">Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="11f61-141">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="11f61-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

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

## <a name="update-data"></a><span data-ttu-id="11f61-142">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="11f61-142">Update data</span></span>
<span data-ttu-id="11f61-143">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="11f61-144">Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="11f61-145">Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="11f61-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="11f61-146">Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="11f61-147">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="11f61-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="11f61-148">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="11f61-148">Delete data</span></span>
<span data-ttu-id="11f61-149">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="11f61-150">Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="11f61-151">Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor.</span><span class="sxs-lookup"><span data-stu-id="11f61-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="11f61-152">Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="11f61-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="11f61-153">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="11f61-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="11f61-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11f61-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="11f61-155">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="11f61-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
