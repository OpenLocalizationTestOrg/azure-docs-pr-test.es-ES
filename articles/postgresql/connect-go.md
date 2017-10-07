---
title: aaaConnect tooAzure base de datos de PostgreSQL mediante el lenguaje Go | Documentos de Microsoft
description: "Este tutorial rápido proporciona un Go programación lenguaje ejemplo puede usar tooconnect y consultar los datos de la base de datos PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a>Base de datos de Azure para PostgreSQL: utilizan el comando Go lenguaje tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan base de datos de Azure para usar PostgreSQL código escrito en hello [vaya](https://golang.org/) language (golang). Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. En este artículo se da por supuesto que está familiarizado con el desarrollo mediante Go, pero que se tooworking nueva con la base de datos de Azure para PostgreSQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Creación de la base de datos: Azure Portal](quickstart-create-server-database-portal.md)
- [Creación de la base de datos: CLI de Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a>Instalación de Go y del conector pq
Instalar [vaya](https://golang.org/doc/install) hello y [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) en su propio equipo. Dependiendo de la plataforma, siga los pasos de hello:

### <a name="windows"></a>Windows
1. [Descargar](https://golang.org/dl/) e instale Go para Microsoft Windows según toohello [las instrucciones de instalación](https://golang.org/doc/install).
2. Inicie símbolo Hola desde el menú de inicio de Hola.
3. Cree una carpeta para su proyecto, como `mkdir  %USERPROFILE%\go\src\postgresqlgo`.
4. Cambie el directorio a la carpeta del proyecto hello, como `cd %USERPROFILE%\go\src\postgresqlgo`.
5. Establezca la variable de entorno de hello para el directorio de código fuente GOPATH toopoint toohello. `set GOPATH=%USERPROFILE%\go`.
6. Instalar hello [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) ejecutando hello `go get github.com/lib/pq` comando.

   En resumen, instale Go, a continuación, ejecute estos comandos en el símbolo del sistema de hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Inicie el shell de Bash Hola. 
2. Instale Go mediante la ejecución de `sudo apt-get install golang-go`.
3. Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/postgresqlgo/`.
4. Cambie el directorio a la carpeta hello, como `cd ~/go/src/postgresqlgo/`.
5. Conjunto hello GOPATH entorno toopoint variable tooa directorio de origen válido, como el principal actual del directorio vaya carpeta. En el shell de bash hello, ejecute `export GOPATH=~/go` tooadd Hola ir directorio como hello GOPATH para la sesión actual de shell de Hola.
6. Instalar hello [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) ejecutando hello `go get github.com/lib/pq` comando.

   En resumen, ejecute estos comandos de Bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a>MacOS de Apple
1. Descargue e instale vayan según toohello [las instrucciones de instalación](https://golang.org/doc/install) coincidencia de la plataforma. 
2. Inicie el shell de Bash Hola. 
3. Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/postgresqlgo/`.
4. Cambie el directorio a la carpeta hello, como `cd ~/go/src/postgresqlgo/`.
5. Conjunto hello GOPATH entorno toopoint variable tooa directorio de origen válido, como el principal actual del directorio vaya carpeta. En el shell de bash hello, ejecute `export GOPATH=~/go` tooadd Hola ir directorio como hello GOPATH para la sesión actual de shell de Hola.
6. Instalar hello [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) ejecutando hello `go get github.com/lib/pq` comando.

   En resumen, instale Go y después ejecute estos comandos de Bash:
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.
3. Haga clic en el nombre del servidor de hello **mypgserver 20170401**.
4. Servidor de hello seleccione **Introducción** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-go/1-connection-string.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **Introducción** página y nombre de inicio de sesión de administrador del servidor de vista Hola. Si es necesario, Hola de restablecimiento de contraseña.

## <a name="build-and-run-go-code"></a>Compilación y ejecución del código de Go 
1. toowrite Golang código, puede utilizar un editor de texto simple, como el Bloc de notas en Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) en Ubuntu o TextEdit en macOS. Si prefiere un entorno de desarrollo integrado (IDE) más rico, pruebe [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft o [Atom](https://atom.io/).
2. Pegue el código de Golang de Hola de secciones de hello debajo de en archivos de texto y guardar en la carpeta del proyecto con la extensión de archivo \*.Vaya, por ejemplo, la ruta de acceso de Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` o ruta de acceso de Linux `~/go/src/postgresqlgo/createtable.go`.
3. Busque hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` constantes en el código de hello y reemplazar los valores de ejemplo de Hola con sus propios valores.  
4. Inicie el símbolo del sistema de Hola o el shell de bash. Cambie el directorio a la carpeta de proyecto. Por ejemplo, en Windows `cd %USERPROFILE%\go\src\postgresqlgo\`. En Linux `cd ~/go/src/postgresqlgo/`. Algunos de los entornos de IDE Hola mencionados ofrecen capacidades de depuración y en tiempo de ejecución sin necesidad de los comandos de shell.
5. Ejecutar código de hello escribiendo el comando hello `go run createtable.go` toocompile Hola aplicación y ejecútela. 
6. O bien, toobuild código de hello en una aplicación nativa, `go build createtable.go`, a continuación, inicie `createtable.exe` aplicación de hello toorun.

## <a name="connect-and-create-a-table"></a>Conexión y creación de una tabla
Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL, seguido de **INSERT INTO** tooadd filas de las instrucciones de SQL en la tabla de Hola.

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) método varias veces toorun varios comandos SQL. Cada vez que un toocheck del método checkError() personalizado si se produjo un error y pánico tooexit si se produce un error.

Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. 

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. consulta select Hola se ejecuta llamando al método [base de datos. Query()](https://golang.org/pkg/database/sql/#DB.Query), y filas resultantes de Hola se mantiene en una variable de tipo [filas](https://golang.org/pkg/database/sql/#Rows). código de Hello lee los valores de datos de columna de Hola de fila actual de hello mediante el método [filas. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) y se aplica a filas hello mediante Hola iterador [filas. Next()](https://golang.org/pkg/database/sql/#Rows.Next) hasta que no hay más filas existen. Valores de columna de cada fila están impresas toohello consola out. Cada vez que un toocheck del método checkError() personalizado si se produjo un error y pánico tooexit si se produce un error.

Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) Hola de toorun método instrucción SQL que actualiza la tabla de Hola. Un toocheck de método checkError() personalizado si se produjo un error y pánico tooexit si un error se produce.

Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. 

código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.

método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola. Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) Hola de toorun método instrucción SQL que actualiza la tabla de Hola. Un toocheck de método checkError() personalizado si se produjo un error y pánico tooexit si un error se produce.

Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./howto-migrate-using-export-and-import.md)
