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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Base de datos de Azure para PostgreSQL: Use Node.js tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos para el uso de PostgreSQL [Node.js](https://nodejs.org/). Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. Hello pasos descritos en este artículo suponen que está familiarizado con el desarrollo utilizando Node.js, y que tooworking nueva con la base de datos de Azure para PostgreSQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Creación de la base de datos: Azure Portal](quickstart-create-server-database-portal.md)
- [Creación de la base de datos: CLI](quickstart-create-server-database-azure-cli.md)

Además, deberá:
- Instalar [Node.js](https://nodejs.org)

## <a name="install-pg-client"></a>Instalación del cliente pg
Instale [pg](https://www.npmjs.com/package/pg), que es un cliente de PostgreSQL para Node.js.

por lo tanto, los toodo ejecutar Administrador de paquetes de nodo de hello (npm) para JavaScript desde el cliente de línea de comandos tooinstall Hola pg.
```bash
npm install pg
```

Comprobar la instalación de hello listado de paquetes de saludo instalados.
```bash
npm list
```

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola que acaba de crear.
3. Haga clic en el nombre del servidor de Hola.
4. Servidor de hello seleccione **Introducción** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-nodejs/1-connection-string.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="running-hello-javascript-code-in-nodejs"></a>Ejecutar código de JavaScript de hello en Node.js
Puede iniciar Node.js Hola intensiva de shell o windows desde línea de comandos escribiendo `node`, a continuación, ejecutar código de JavaScript de ejemplo de Hola de forma interactiva mediante copia y pegar en el símbolo del sistema de Hola. Como alternativa, puede guardar código de JavaScript de hello en un archivo de texto e inicie `node filename.js` con el nombre de archivo de Hola como un parámetro toorun.

## <a name="connect-create-table-and-insert-data"></a>Conexión, creación de una tabla e inserción de datos
Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL.
Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL. Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor. Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL. 

Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

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

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL. Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor. Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL. 

Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

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

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL. Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL. Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor. Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL. 

Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

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

## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. Hola [pg. Cliente](https://github.com/brianc/node-postgres/wiki/Client) objeto es toointerface usado con el servidor de hello PostgreSQL. Hola [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) función es tooestablish usado Hola de conexión toohello del servidor. Hola [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL. 

Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

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

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./howto-migrate-using-export-and-import.md)
