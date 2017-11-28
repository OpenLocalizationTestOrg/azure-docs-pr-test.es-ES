---
title: "Conexión a Azure Database for MySQL mediante Go | Microsoft Docs"
description: "En este tutorial rápido se proporcionan ejemplos de código Go que se pueden usar para conectarse a Azure Database for MySQL y consultar datos en este servicio."
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
ms.openlocfilehash: 42a6b1c37de08971674c8b38f1e13bfd657f8b03
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="26343-103">Azure Database for MySQL: uso del lenguaje Go para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="26343-103">Azure Database for MySQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="26343-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for MySQL mediante código escrito en el lenguaje [Go](https://golang.org/) desde las plataformas Windows, Ubuntu Linux y macOS de Apple.</span><span class="sxs-lookup"><span data-stu-id="26343-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using code written in the [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="26343-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="26343-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="26343-106">En este artículo se da por hecho que está familiarizado con el desarrollo mediante Go, pero que nunca ha usado Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="26343-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26343-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="26343-107">Prerequisites</span></span>
<span data-ttu-id="26343-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="26343-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="26343-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="26343-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="26343-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="26343-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="26343-111">Instalación de Go y el conector de MySQL</span><span class="sxs-lookup"><span data-stu-id="26343-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="26343-112">Instale [Go](https://golang.org/doc/install) y [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) en su propia máquina.</span><span class="sxs-lookup"><span data-stu-id="26343-112">Install [Go](https://golang.org/doc/install) and the [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="26343-113">Dependiendo de la plataforma, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="26343-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="26343-114">Windows</span><span class="sxs-lookup"><span data-stu-id="26343-114">Windows</span></span>
1. <span data-ttu-id="26343-115">[Descargue](https://golang.org/dl/) e instale Go para Microsoft Windows de acuerdo con las [instrucciones de instalación](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="26343-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="26343-116">En el menú Inicio, inicie el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="26343-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="26343-117">Cree una carpeta para su proyecto, como</span><span class="sxs-lookup"><span data-stu-id="26343-117">Make a folder for your project such.</span></span> <span data-ttu-id="26343-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="26343-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="26343-119">Cambie el directorio a la carpeta de proyecto, por ejemplo `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="26343-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="26343-120">Establezca la variable de entorno para GOPATH con el fin de que apunte al directorio de código fuente.</span><span class="sxs-lookup"><span data-stu-id="26343-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="26343-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="26343-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="26343-122">Instale [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) mediante la ejecución del comando `go get github.com/go-sql-driver/mysql`.</span><span class="sxs-lookup"><span data-stu-id="26343-122">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="26343-123">En resumen, instale Go y después ejecute estos comandos en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="26343-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="26343-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="26343-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="26343-125">Inicie el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="26343-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="26343-126">Instale Go mediante la ejecución de `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="26343-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="26343-127">Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="26343-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="26343-128">Cambie el directorio a la carpeta, por ejemplo, `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="26343-128">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="26343-129">Establezca la variable de entorno GOPATH para que apunte a un directorio de origen válido, como la carpeta go del directorio principal actual.</span><span class="sxs-lookup"><span data-stu-id="26343-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="26343-130">En el shell de Bash, ejecute `export GOPATH=~/go` para agregar el directorio go como GOPATH para la sesión de shell actual.</span><span class="sxs-lookup"><span data-stu-id="26343-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="26343-131">Instale [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) mediante la ejecución del comando `go get github.com/go-sql-driver/mysql`.</span><span class="sxs-lookup"><span data-stu-id="26343-131">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="26343-132">En resumen, ejecute estos comandos de Bash:</span><span class="sxs-lookup"><span data-stu-id="26343-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="26343-133">MacOS de Apple</span><span class="sxs-lookup"><span data-stu-id="26343-133">Apple macOS</span></span>
1. <span data-ttu-id="26343-134">Descargue e instale Go de acuerdo con las [instrucciones de instalación](https://golang.org/doc/install) que coincidan con su plataforma.</span><span class="sxs-lookup"><span data-stu-id="26343-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="26343-135">Inicie el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="26343-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="26343-136">Cree una carpeta para el proyecto en su directorio principal, como `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="26343-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="26343-137">Cambie el directorio a la carpeta, por ejemplo, `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="26343-137">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="26343-138">Establezca la variable de entorno GOPATH para que apunte a un directorio de origen válido, como la carpeta go del directorio principal actual.</span><span class="sxs-lookup"><span data-stu-id="26343-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="26343-139">En el shell de Bash, ejecute `export GOPATH=~/go` para agregar el directorio go como GOPATH para la sesión de shell actual.</span><span class="sxs-lookup"><span data-stu-id="26343-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="26343-140">Instale [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) mediante la ejecución del comando `go get github.com/go-sql-driver/mysql`.</span><span class="sxs-lookup"><span data-stu-id="26343-140">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="26343-141">En resumen, instale Go y después ejecute estos comandos de Bash:</span><span class="sxs-lookup"><span data-stu-id="26343-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="26343-142">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="26343-142">Get connection information</span></span>
<span data-ttu-id="26343-143">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="26343-143">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="26343-144">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="26343-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="26343-145">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="26343-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="26343-146">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que ha creado, por ejemplo, **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="26343-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="26343-147">Haga clic en el nombre del servidor **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="26343-147">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="26343-148">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="26343-148">Select the server's **Properties** page.</span></span> <span data-ttu-id="26343-149">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="26343-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="26343-150">![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="26343-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="26343-151">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="26343-151">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="26343-152">Compilación y ejecución del código de Go</span><span class="sxs-lookup"><span data-stu-id="26343-152">Build and run Go code</span></span> 
1. <span data-ttu-id="26343-153">Para escribir código Golang, utilice un editor de texto simple, como el Bloc de notas en Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) en Ubuntu, o TextEdit en macOS.</span><span class="sxs-lookup"><span data-stu-id="26343-153">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="26343-154">Si prefiere un entorno de desarrollo integrado (IDE) más rico, pruebe [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="26343-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="26343-155">Pegue el código de Go de las secciones siguientes en archivos de texto y guárdelos en la carpeta del proyecto con la extensión de archivo \*.go, como la ruta de acceso de Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` o la ruta de acceso de Linux `~/go/src/mysqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="26343-155">Paste the Go code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="26343-156">Busque las constantes `HOST`, `DATABASE`, `USER` y `PASSWORD` en el código y reemplace los valores de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="26343-156">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span> 
4. <span data-ttu-id="26343-157">Inicie el símbolo del sistema o el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="26343-157">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="26343-158">Cambie el directorio a la carpeta de proyecto.</span><span class="sxs-lookup"><span data-stu-id="26343-158">Change directory into your project folder.</span></span> <span data-ttu-id="26343-159">Por ejemplo, en Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="26343-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="26343-160">En Linux `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="26343-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="26343-161">Algunos de los editores de IDE mencionados ofrecen funcionalidades de depuración y de tiempo de ejecución sin necesidad de comandos de shell.</span><span class="sxs-lookup"><span data-stu-id="26343-161">Some of the IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="26343-162">Ejecute el código escribiendo el comando `go run createtable.go` para compilar la aplicación y ejecútela.</span><span class="sxs-lookup"><span data-stu-id="26343-162">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="26343-163">Además, para compilar el código en una aplicación nativa, `go build createtable.go`, inicie `createtable.exe` para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="26343-163">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="26343-164">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="26343-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="26343-165">Use el código siguiente para conectarse al servidor, crear una tabla y cargar los datos mediante una instrucción SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="26343-165">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="26343-166">El código importa tres paquetes: el [paquete sql](https://golang.org/pkg/database/sql/), el [paquete go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) como controlador para la comunicación con Azure Database for MySQL y el [paquete fmt](https://golang.org/pkg/fmt/) para la entrada y salida impresas en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="26343-166">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="26343-167">El código llama al método [sql.Open()](http://go-database-sql.org/accessing.html) para conectarse a Azure Database for MySQL y comprueba la conexión mediante el método [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="26343-167">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="26343-168">Durante todo el proceso se usa un [identificador de base de datos](https://golang.org/pkg/database/sql/#DB), que contiene el grupo de conexiones del servidor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="26343-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="26343-169">El código llama al método [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) varias veces para ejecutar varios comandos DDL.</span><span class="sxs-lookup"><span data-stu-id="26343-169">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several DDL commands.</span></span> <span data-ttu-id="26343-170">El código también usa los métodos [Prepare()](http://go-database-sql.org/prepared.html) y Exec() para ejecutar instrucciones preparadas con diferentes parámetros para insertar tres filas.</span><span class="sxs-lookup"><span data-stu-id="26343-170">The code also uses the [Prepare()](http://go-database-sql.org/prepared.html) and Exec() to run prepared statements with different parameters to insert three rows.</span></span> <span data-ttu-id="26343-171">En cada una de las veces se usa un método checkError() personalizado para comprobar si se ha producido un error y, en caso afirmativo, avisa para salir.</span><span class="sxs-lookup"><span data-stu-id="26343-171">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="26343-172">Reemplace las constantes `host`, `database`, `user` y `password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="26343-172">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

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

## <a name="read-data"></a><span data-ttu-id="26343-173">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="26343-173">Read data</span></span>
<span data-ttu-id="26343-174">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="26343-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="26343-175">El código importa tres paquetes: el [paquete sql](https://golang.org/pkg/database/sql/), el [paquete go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) como controlador para la comunicación con Azure Database for MySQL y el [paquete fmt](https://golang.org/pkg/fmt/) para la entrada y salida impresas en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="26343-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="26343-176">El código llama al método [sql.Open()](http://go-database-sql.org/accessing.html) para conectarse a Azure Database for MySQL y comprueba la conexión mediante el método [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="26343-176">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="26343-177">Durante todo el proceso se usa un [identificador de base de datos](https://golang.org/pkg/database/sql/#DB), que contiene el grupo de conexiones del servidor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="26343-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="26343-178">El código llama al método [Query()](https://golang.org/pkg/database/sql/#DB.Query) para ejecutar el comando select.</span><span class="sxs-lookup"><span data-stu-id="26343-178">The code calls the [Query()](https://golang.org/pkg/database/sql/#DB.Query) method to run the select command.</span></span> <span data-ttu-id="26343-179">A continuación, ejecuta [Next()](https://golang.org/pkg/database/sql/#Rows.Next) para recorrer en iteración el conjunto de resultados y [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) para analizar los valores de columna y guardar el valor en variables.</span><span class="sxs-lookup"><span data-stu-id="26343-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) to iterate through the result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) to parse the column values, saving the value into variables.</span></span> <span data-ttu-id="26343-180">En cada una de las veces se usa un método checkError() personalizado para comprobar si se ha producido un error y, en caso afirmativo, avisa para salir.</span><span class="sxs-lookup"><span data-stu-id="26343-180">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="26343-181">Reemplace las constantes `host`, `database`, `user` y `password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="26343-181">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from the table.
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

## <a name="update-data"></a><span data-ttu-id="26343-182">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="26343-182">Update data</span></span>
<span data-ttu-id="26343-183">Use el código siguiente para conectarse y actualizar los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="26343-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="26343-184">El código importa tres paquetes: el [paquete sql](https://golang.org/pkg/database/sql/), el [paquete go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) como controlador para la comunicación con Azure Database for MySQL y el [paquete fmt](https://golang.org/pkg/fmt/) para la entrada y salida impresas en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="26343-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="26343-185">El código llama al método [sql.Open()](http://go-database-sql.org/accessing.html) para conectarse a Azure Database for MySQL y comprueba la conexión mediante el método [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="26343-185">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="26343-186">Durante todo el proceso se usa un [identificador de base de datos](https://golang.org/pkg/database/sql/#DB), que contiene el grupo de conexiones del servidor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="26343-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="26343-187">El código llama al método [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) para ejecutar el comando update.</span><span class="sxs-lookup"><span data-stu-id="26343-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the update command.</span></span> <span data-ttu-id="26343-188">En cada una de las veces se usa un método checkError() personalizado para comprobar si se ha producido un error y, en caso afirmativo, avisa para salir.</span><span class="sxs-lookup"><span data-stu-id="26343-188">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="26343-189">Reemplace las constantes `host`, `database`, `user` y `password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="26343-189">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="26343-190">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="26343-190">Delete data</span></span>
<span data-ttu-id="26343-191">Use el código siguiente para conectarse y eliminar datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="26343-191">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="26343-192">El código importa tres paquetes: el [paquete sql](https://golang.org/pkg/database/sql/), el [paquete go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) como controlador para la comunicación con Azure Database for MySQL y el [paquete fmt](https://golang.org/pkg/fmt/) para la entrada y salida impresas en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="26343-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="26343-193">El código llama al método [sql.Open()](http://go-database-sql.org/accessing.html) para conectarse a Azure Database for MySQL y comprueba la conexión mediante el método [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="26343-193">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="26343-194">Durante todo el proceso se usa un [identificador de base de datos](https://golang.org/pkg/database/sql/#DB), que contiene el grupo de conexiones del servidor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="26343-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="26343-195">El código llama al método [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) para ejecutar el comando delete.</span><span class="sxs-lookup"><span data-stu-id="26343-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the delete command.</span></span> <span data-ttu-id="26343-196">En cada una de las veces se usa un método checkError() personalizado para comprobar si se ha producido un error y, en caso afirmativo, avisa para salir.</span><span class="sxs-lookup"><span data-stu-id="26343-196">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="26343-197">Reemplace las constantes `host`, `database`, `user` y `password` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="26343-197">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="26343-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26343-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="26343-199">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="26343-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
