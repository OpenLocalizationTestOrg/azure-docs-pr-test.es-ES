---
title: Conectar tooAzure base de datos de MySQL mediante Ir | Documentos de Microsoft
description: "Este tutorial rápido proporciona varios ejemplos de código de Go puede usar tooconnect y consultar los datos de la base de datos MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a>Base de datos de Azure para MySQL: utilizan el comando Go lenguaje tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan base de datos de Azure para el uso de MySQL código escrito en hello [vaya](https://golang.org/) idioma de Windows, Ubuntu Linux y Apple plataformas macOS. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. En este artículo se da por supuesto que está familiarizado con el desarrollo mediante Go, pero que se tooworking nueva con la base de datos de Azure para MySQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

## <a name="install-go-and-mysql-connector"></a>Instalación de Go y el conector de MySQL
Instalar [vaya](https://golang.org/doc/install) hello y [go--controlador sql para MySQL](https://github.com/go-sql-driver/mysql#installation) en su propio equipo. Dependiendo de la plataforma, siga los pasos de hello:

### <a name="windows"></a>Windows
1. [Descargar](https://golang.org/dl/) e instale Go para Microsoft Windows según toohello [las instrucciones de instalación](https://golang.org/doc/install).
2. Inicie símbolo Hola desde el menú de inicio de Hola.
3. Cree una carpeta para su proyecto, como `mkdir  %USERPROFILE%\go\src\mysqlgo`.
4. Cambie el directorio a la carpeta del proyecto hello, como `cd %USERPROFILE%\go\src\mysqlgo`.
5. Establezca la variable de entorno de hello para el directorio de código fuente GOPATH toopoint toohello. `set GOPATH=%USERPROFILE%\go`.
6. Instalar hello [go--controlador sql para mysql](https://github.com/go-sql-driver/mysql#installation) ejecutando hello `go get github.com/go-sql-driver/mysql` comando.

   En resumen, instale Go, a continuación, ejecute estos comandos en el símbolo del sistema de hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Inicie el shell de Bash Hola. 
2. Instale Go mediante la ejecución de `sudo apt-get install golang-go`.
3. Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/mysqlgo/`.
4. Cambie el directorio a la carpeta hello, como `cd ~/go/src/mysqlgo/`.
5. Conjunto hello GOPATH entorno toopoint variable tooa directorio de origen válido, como el principal actual del directorio vaya carpeta. En el shell de bash hello, ejecute `export GOPATH=~/go` tooadd Hola ir directorio como hello GOPATH para la sesión actual de shell de Hola.
6. Instalar hello [go--controlador sql para mysql](https://github.com/go-sql-driver/mysql#installation) ejecutando hello `go get github.com/go-sql-driver/mysql` comando.

   En resumen, ejecute estos comandos de Bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a>MacOS de Apple
1. Descargue e instale vayan según toohello [las instrucciones de instalación](https://golang.org/doc/install) coincidencia de la plataforma. 
2. Inicie el shell de Bash Hola. 
3. Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/mysqlgo/`.
4. Cambie el directorio a la carpeta hello, como `cd ~/go/src/mysqlgo/`.
5. Conjunto hello GOPATH entorno toopoint variable tooa directorio de origen válido, como el principal actual del directorio vaya carpeta. En el shell de bash hello, ejecute `export GOPATH=~/go` tooadd Hola ir directorio como hello GOPATH para la sesión actual de shell de Hola.
6. Instalar hello [go--controlador sql para mysql](https://github.com/go-sql-driver/mysql#installation) ejecutando hello `go get github.com/go-sql-driver/mysql` comando.

   En resumen, instale Go y después ejecute estos comandos de Bash:
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque servidor hello plegado, como **myserver4demo**.
3. Haga clic en el nombre del servidor de hello **myserver4demo**.
4. Servidor de hello seleccione **propiedades** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-go/1_server-properties-name-login.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.
   

## <a name="build-and-run-go-code"></a>Compilación y ejecución del código de Go 
1. toowrite Golang código, puede utilizar un editor de texto simple, como el Bloc de notas en Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) en Ubuntu o TextEdit en macOS. Si prefiere un entorno de desarrollo integrado (IDE) más rico, pruebe [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft o [Atom](https://atom.io/).
2. Pegue Hola código Go de secciones de hello debajo de en archivos de texto y guarde en la carpeta del proyecto con la extensión de archivo \*.Vaya, por ejemplo, la ruta de acceso de Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` o ruta de acceso de Linux `~/go/src/mysqlgo/createtable.go`.
3. Busque hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` constantes en el código de hello y reemplazar los valores de ejemplo de Hola con sus propios valores. 
4. Inicie el símbolo del sistema de Hola o el shell de bash. Cambie el directorio a la carpeta de proyecto. Por ejemplo, en Windows `cd %USERPROFILE%\go\src\mysqlgo\`. En Linux `cd ~/go/src/mysqlgo/`.  Algunos editores de IDE Hola mencionados ofrecen capacidades de depuración y en tiempo de ejecución sin necesidad de los comandos de shell.
5. Ejecutar código de hello escribiendo el comando hello `go run createtable.go` toocompile Hola aplicación y ejecútela. 
6. O bien, toobuild código de hello en una aplicación nativa, `go build createtable.go`, a continuación, inicie `createtable.exe` aplicación de hello toorun.

## <a name="connect-create-table-and-insert-data"></a>Conexión, creación de una tabla e inserción de datos
Siguiente Hola de uso codificar tooconnect toohello server, cree una tabla y cargar datos de hello mediante un **insertar** instrucción SQL. 

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [controlador de sql vaya para mysql](https://github.com/go-sql-driver/mysql#installation) como un toocommunicate de controlador con base de datos de Azure para MySQL Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/)para impreso entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de datos MySQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) método varias veces toorun varios comandos DDL. código de Hello también usa hello [Prepare()](http://go-database-sql.org/prepared.html) y Exec() toorun preparado instrucciones con parámetros diferentes tooinsert tres filas. Cada vez que un método checkError() personalizado es toocheck usado si se produjo un error y pánico tooexit.

Reemplace hello `host`, `database`, `user`, y `password` constantes con sus propios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. 

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [controlador de sql vaya para mysql](https://github.com/go-sql-driver/mysql#installation) como un toocommunicate de controlador con base de datos de Azure para MySQL Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/)para impreso entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de datos MySQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. Hola de llamadas de código de Hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) comando select de método toorun Hola. A continuación, ejecuta [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate a través del conjunto de resultados de Hola y [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse Hola valores de las columnas, guardar el valor de hello en variables. Cada vez que un método checkError() personalizado es toocheck usado si se produjo un error y pánico tooexit.

Reemplace hello `host`, `database`, `user`, y `password` constantes con sus propios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL. 

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [controlador de sql vaya para mysql](https://github.com/go-sql-driver/mysql#installation) como un toocommunicate de controlador con base de datos de Azure para MySQL Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/)para impreso entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de datos MySQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) comando de actualización de método toorun Hola. Cada vez que un método checkError() personalizado es toocheck usado si se produjo un error y pánico tooexit.

Reemplace hello `host`, `database`, `user`, y `password` constantes con sus propios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y eliminar los datos mediante un **eliminar** instrucción SQL. 

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [controlador de sql vaya para mysql](https://github.com/go-sql-driver/mysql#installation) como un toocommunicate de controlador con base de datos de Azure para MySQL Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/)para impreso entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de datos MySQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) Hola de método toorun comando delete. Cada vez que un método checkError() personalizado es toocheck usado si se produjo un error y pánico tooexit.

Reemplace hello `host`, `database`, `user`, y `password` constantes con sus propios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./concepts-migrate-import-export.md)
