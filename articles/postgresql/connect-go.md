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
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="07a82-103">Base de datos de Azure para PostgreSQL: utilizan el comando Go lenguaje tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="07a82-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="07a82-104">Este tutorial rápido muestra cómo tooconnect tooan base de datos de Azure para usar PostgreSQL código escrito en hello [vaya](https://golang.org/) language (golang).</span><span class="sxs-lookup"><span data-stu-id="07a82-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="07a82-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="07a82-106">En este artículo se da por supuesto que está familiarizado con el desarrollo mediante Go, pero que se tooworking nueva con la base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07a82-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07a82-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07a82-107">Prerequisites</span></span>
<span data-ttu-id="07a82-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="07a82-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="07a82-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="07a82-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="07a82-110">Creación de la base de datos: CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="07a82-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="07a82-111">Instalación de Go y del conector pq</span><span class="sxs-lookup"><span data-stu-id="07a82-111">Install Go and pq connector</span></span>
<span data-ttu-id="07a82-112">Instalar [vaya](https://golang.org/doc/install) hello y [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) en su propio equipo.</span><span class="sxs-lookup"><span data-stu-id="07a82-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="07a82-113">Dependiendo de la plataforma, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="07a82-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="07a82-114">Windows</span><span class="sxs-lookup"><span data-stu-id="07a82-114">Windows</span></span>
1. <span data-ttu-id="07a82-115">[Descargar](https://golang.org/dl/) e instale Go para Microsoft Windows según toohello [las instrucciones de instalación](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="07a82-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="07a82-116">Inicie símbolo Hola desde el menú de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="07a82-117">Cree una carpeta para su proyecto, como</span><span class="sxs-lookup"><span data-stu-id="07a82-117">Make a folder for your project such.</span></span> <span data-ttu-id="07a82-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="07a82-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="07a82-119">Cambie el directorio a la carpeta del proyecto hello, como `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="07a82-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="07a82-120">Establezca la variable de entorno de hello para el directorio de código fuente GOPATH toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="07a82-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="07a82-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="07a82-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="07a82-122">Instalar hello [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) ejecutando hello `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="07a82-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="07a82-123">En resumen, instale Go, a continuación, ejecute estos comandos en el símbolo del sistema de hello:</span><span class="sxs-lookup"><span data-stu-id="07a82-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="07a82-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="07a82-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="07a82-125">Inicie el shell de Bash Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="07a82-126">Instale Go mediante la ejecución de `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="07a82-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="07a82-127">Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="07a82-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="07a82-128">Cambie el directorio a la carpeta hello, como `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="07a82-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="07a82-129">Conjunto hello GOPATH entorno toopoint variable tooa directorio de origen válido, como el principal actual del directorio vaya carpeta.</span><span class="sxs-lookup"><span data-stu-id="07a82-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="07a82-130">En el shell de bash hello, ejecute `export GOPATH=~/go` tooadd Hola ir directorio como hello GOPATH para la sesión actual de shell de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="07a82-131">Instalar hello [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) ejecutando hello `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="07a82-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="07a82-132">En resumen, ejecute estos comandos de Bash:</span><span class="sxs-lookup"><span data-stu-id="07a82-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="07a82-133">MacOS de Apple</span><span class="sxs-lookup"><span data-stu-id="07a82-133">Apple macOS</span></span>
1. <span data-ttu-id="07a82-134">Descargue e instale vayan según toohello [las instrucciones de instalación](https://golang.org/doc/install) coincidencia de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="07a82-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="07a82-135">Inicie el shell de Bash Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="07a82-136">Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="07a82-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="07a82-137">Cambie el directorio a la carpeta hello, como `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="07a82-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="07a82-138">Conjunto hello GOPATH entorno toopoint variable tooa directorio de origen válido, como el principal actual del directorio vaya carpeta.</span><span class="sxs-lookup"><span data-stu-id="07a82-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="07a82-139">En el shell de bash hello, ejecute `export GOPATH=~/go` tooadd Hola ir directorio como hello GOPATH para la sesión actual de shell de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="07a82-140">Instalar hello [controlador Postgres vaya pura (pq)](https://github.com/lib/pq) ejecutando hello `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="07a82-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="07a82-141">En resumen, instale Go y después ejecute estos comandos de Bash:</span><span class="sxs-lookup"><span data-stu-id="07a82-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="07a82-142">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="07a82-142">Get connection information</span></span>
<span data-ttu-id="07a82-143">Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="07a82-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="07a82-144">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="07a82-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="07a82-145">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="07a82-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="07a82-146">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="07a82-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="07a82-147">Haga clic en el nombre del servidor de hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="07a82-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="07a82-148">Servidor de hello seleccione **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="07a82-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="07a82-149">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="07a82-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="07a82-150">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="07a82-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="07a82-151">Si olvida su información de inicio de sesión de servidor, vaya a toohello **Introducción** página y nombre de inicio de sesión de administrador del servidor de vista Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="07a82-152">Si es necesario, Hola de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="07a82-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="07a82-153">Compilación y ejecución del código de Go</span><span class="sxs-lookup"><span data-stu-id="07a82-153">Build and run Go code</span></span> 
1. <span data-ttu-id="07a82-154">toowrite Golang código, puede utilizar un editor de texto simple, como el Bloc de notas en Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) en Ubuntu o TextEdit en macOS.</span><span class="sxs-lookup"><span data-stu-id="07a82-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="07a82-155">Si prefiere un entorno de desarrollo integrado (IDE) más rico, pruebe [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="07a82-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="07a82-156">Pegue el código de Golang de Hola de secciones de hello debajo de en archivos de texto y guardar en la carpeta del proyecto con la extensión de archivo \*.Vaya, por ejemplo, la ruta de acceso de Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` o ruta de acceso de Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="07a82-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="07a82-157">Busque hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` constantes en el código de hello y reemplazar los valores de ejemplo de Hola con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="07a82-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="07a82-158">Inicie el símbolo del sistema de Hola o el shell de bash.</span><span class="sxs-lookup"><span data-stu-id="07a82-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="07a82-159">Cambie el directorio a la carpeta de proyecto.</span><span class="sxs-lookup"><span data-stu-id="07a82-159">Change directory into your project folder.</span></span> <span data-ttu-id="07a82-160">Por ejemplo, en Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="07a82-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="07a82-161">En Linux `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="07a82-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="07a82-162">Algunos de los entornos de IDE Hola mencionados ofrecen capacidades de depuración y en tiempo de ejecución sin necesidad de los comandos de shell.</span><span class="sxs-lookup"><span data-stu-id="07a82-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="07a82-163">Ejecutar código de hello escribiendo el comando hello `go run createtable.go` toocompile Hola aplicación y ejecútela.</span><span class="sxs-lookup"><span data-stu-id="07a82-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="07a82-164">O bien, toobuild código de hello en una aplicación nativa, `go build createtable.go`, a continuación, inicie `createtable.exe` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="07a82-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="07a82-165">Conexión y creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="07a82-165">Connect and create a table</span></span>
<span data-ttu-id="07a82-166">Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL, seguido de **INSERT INTO** tooadd filas de las instrucciones de SQL en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="07a82-167">código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="07a82-168">método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="07a82-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="07a82-169">A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="07a82-170">Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) método varias veces toorun varios comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="07a82-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="07a82-171">Cada vez que un toocheck del método checkError() personalizado si se produjo un error y pánico tooexit si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="07a82-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="07a82-172">Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="07a82-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="07a82-173">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="07a82-173">Read data</span></span>
<span data-ttu-id="07a82-174">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="07a82-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="07a82-175">código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="07a82-176">método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="07a82-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="07a82-177">A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="07a82-178">consulta select Hola se ejecuta llamando al método [base de datos. Query()](https://golang.org/pkg/database/sql/#DB.Query), y filas resultantes de Hola se mantiene en una variable de tipo [filas](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="07a82-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="07a82-179">código de Hello lee los valores de datos de columna de Hola de fila actual de hello mediante el método [filas. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) y se aplica a filas hello mediante Hola iterador [filas. Next()](https://golang.org/pkg/database/sql/#Rows.Next) hasta que no hay más filas existen.</span><span class="sxs-lookup"><span data-stu-id="07a82-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="07a82-180">Valores de columna de cada fila están impresas toohello consola out. Cada vez que un toocheck del método checkError() personalizado si se produjo un error y pánico tooexit si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="07a82-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="07a82-181">Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="07a82-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="07a82-182">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="07a82-182">Update data</span></span>
<span data-ttu-id="07a82-183">Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="07a82-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="07a82-184">código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="07a82-185">método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="07a82-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="07a82-186">A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="07a82-187">Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) Hola de toorun método instrucción SQL que actualiza la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="07a82-188">Un toocheck de método checkError() personalizado si se produjo un error y pánico tooexit si un error se produce.</span><span class="sxs-lookup"><span data-stu-id="07a82-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="07a82-189">Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="07a82-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="delete-data"></a><span data-ttu-id="07a82-190">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="07a82-190">Delete data</span></span>
<span data-ttu-id="07a82-191">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="07a82-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="07a82-192">código de Hello importa tres paquetes: Hola [paquete sql](https://golang.org/pkg/database/sql/), hello [paquete pq](http://godoc.org/github.com/lib/pq) como un toocommunicate de controlador con servidor de Postgres Hola y Hola [fmt paquete](https://golang.org/pkg/fmt/) para imprimir entrada y salida en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="07a82-193">método llama a código de Hello [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de datos de PostgreSQL y comprobaciones de hello conexión mediante el método [base de datos. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="07a82-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="07a82-194">A [identificador de base de datos](https://golang.org/pkg/database/sql/#DB) se utiliza en su totalidad, que contiene el grupo de conexiones de hello para el servidor de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="07a82-195">Hola de llamadas de código de Hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) Hola de toorun método instrucción SQL que actualiza la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="07a82-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="07a82-196">Un toocheck de método checkError() personalizado si se produjo un error y pánico tooexit si un error se produce.</span><span class="sxs-lookup"><span data-stu-id="07a82-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="07a82-197">Reemplace hello `HOST`, `DATABASE`, `USER`, y `PASSWORD` parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="07a82-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="07a82-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07a82-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="07a82-199">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="07a82-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
