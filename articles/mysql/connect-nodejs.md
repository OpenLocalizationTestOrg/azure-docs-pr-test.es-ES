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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Base de datos de Azure para MySQL: Use Node.js tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos para el uso de MySQL [Node.js](https://nodejs.org/) entre plataformas de Windows, Ubuntu Linux y Mac. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. Hello pasos descritos en este artículo suponen que está familiarizado con el desarrollo utilizando Node.js, y que tooworking nueva con la base de datos de Azure para MySQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

Además, deberá:
- Instalar hello [Node.js](https://nodejs.org) en tiempo de ejecución.
- Instalar [mysql2](https://www.npmjs.com/package/mysql2) tooconnect tooMySQL de hello aplicación Node.js del paquete. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Instalar Node.js y Hola conector MySQL
Dependiendo de la plataforma, siga Hola instrucciones apropiadas tooinstall Node.js. Usar npm tooinstall hello mysql2 paquete y sus dependencias en la carpeta del proyecto.

### <a name="windows"></a>**Windows**
1. Visite hello [página de descargas de Node.js](https://nodejs.org/en/download/) y seleccione la opción deseada del instalador de Windows.
2. Cree una carpeta de proyecto local, como `nodejsmysql`. 
3. Inicie símbolo hello y cd en la carpeta del proyecto hello, como`cd c:\nodejsmysql\`
4. Ejecute biblioteca de hello NPM herramienta tooinstall hello mysql2 en la carpeta del proyecto Hola.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Comprobar instalación Hola Hola `npm list` salida de texto para `mysql2@1.3.5`.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. Siguiente ejecución Hola comandos tooinstall **Node.js** y **npm** Administrador de paquetes de saludo para Node.js.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Ejecute hello después comandos toomake una carpeta de proyecto `mysqlnodejs` e instale el paquete de mysql2 de hello en esa carpeta.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Comprobar la instalación de hello activando el texto de salida de la lista de npm para `mysql2@1.3.5`.

### <a name="mac-os"></a>**Mac OS**
1. Escriba Hola después comandos tooinstall **brew**, un administrador de paquetes de fácil de usar para Mac OS X y **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Ejecute hello después comandos toomake una carpeta de proyecto `mysqlnodejs` e instale el paquete de mysql2 de hello en esa carpeta.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Comprobar instalación Hola Hola `npm list` salida de texto para `mysql2@1.3.6`. Hello número de versión puede variar a medida que se publiquen nuevas revisiones.

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el panel izquierdo de hello, haga clic en **todos los recursos**y, a continuación, busque servidor Hola se haya creado (por ejemplo, **myserver4demo**).
3. Haga clic en el nombre del servidor de hello **myserver4demo**.
4. Servidor de hello seleccione **propiedades** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-nodejs/1_server-properties-name-login.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="running-hello-javascript-code-in-nodejs"></a>Ejecutar código de JavaScript de hello en Node.js
1. Pegue el código de JavaScript de hello en archivos de texto y guarde en una carpeta del proyecto con .js de extensión de archivo, como C:\nodejsmysql\createtable.js o /home/username/nodejsmysql/createtable.js
2. Inicie el símbolo del sistema de Hola o el shell de bash. Cambie el directorio a la carpeta de proyecto `cd nodejsmysql`.
3. aplicación de hello toorun, escriba Hola nodo comando seguido por nombre de archivo de hello, como `node createtable.js`.
4. En Windows, si la aplicación de nodo de hello no está en la ruta de la variable de entorno, puede necesita toouse Hola ruta de acceso completa toolaunch Hola nodo aplicación, como`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>Conexión, creación de una tabla e inserción de datos
Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL.

Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola. Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) función es tooestablish usado Hola de conexión toohello del servidor. Hola [query()](https://github.com/mysqljs/mysql#performing-queries) función es consulta SQL hello tooexecute usado en la base de datos MySQL. 

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

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

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. 

Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola. Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) método es tooestablish usado Hola de conexión toohello del servidor. Hola [query()](https://github.com/mysqljs/mysql#performing-queries) método es consulta SQL hello tooexecute usado en la base de datos MySQL. matriz de resultados de Hello es toohold usado Hola resultados de consulta de Hola.

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

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

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL. 

Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola. Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) método es tooestablish usado Hola de conexión toohello del servidor. Hola [query()](https://github.com/mysqljs/mysql#performing-queries) método es consulta SQL hello tooexecute usado en la base de datos MySQL. 

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

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

## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. 

Hola [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) método es toointerface usado con el servidor de MySQL Hola. Hola [connect()](https://github.com/mysqljs/mysql#establishing-connections) método es tooestablish usado Hola de conexión toohello del servidor. Hola [query()](https://github.com/mysqljs/mysql#performing-queries) método es consulta SQL hello tooexecute usado en la base de datos MySQL. 

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

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

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./concepts-migrate-import-export.md)
