---
title: aaaConnect tooAzure base de datos de PostgreSQL mediante Ruby | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo de código Ruby puede usar tooconnect y consultar los datos de la base de datos PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="39753-103">Base de datos de Azure para PostgreSQL: Use Ruby tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="39753-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="39753-104">Este tutorial rápido muestra cómo tooconnect tooan Azure base de datos PostgreSQL utilizando un [Ruby](https://www.ruby-lang.org) aplicación.</span><span class="sxs-lookup"><span data-stu-id="39753-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="39753-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="39753-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="39753-106">En este artículo se da por supuesto que está familiarizado con el desarrollo mediante Ruby, pero que se tooworking nueva con la base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="39753-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39753-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="39753-107">Prerequisites</span></span>
<span data-ttu-id="39753-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="39753-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="39753-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="39753-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="39753-110">Creación de la base de datos: CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="39753-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="39753-111">Instalación de Ruby</span><span class="sxs-lookup"><span data-stu-id="39753-111">Install Ruby</span></span>
<span data-ttu-id="39753-112">Instale Ruby en su propia máquina.</span><span class="sxs-lookup"><span data-stu-id="39753-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="39753-113">Windows</span><span class="sxs-lookup"><span data-stu-id="39753-113">Windows</span></span>
- <span data-ttu-id="39753-114">Descarga e instale Hola versión más reciente de [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="39753-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="39753-115">En hello, finalizar la pantalla del instalador MSI de hello, casilla Hola que dice "ejecución 'ridk instalar' tooinstall MSYS2 y cadena de herramientas de desarrollo".</span><span class="sxs-lookup"><span data-stu-id="39753-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="39753-116">A continuación, haga clic en **finalizar** instalador de toolaunch Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="39753-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="39753-117">se inicia el instalador de RubyInstaller2 para Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="39753-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="39753-118">Tipo de actualización de repositorio de hello MSYS2 tooinstall 2.</span><span class="sxs-lookup"><span data-stu-id="39753-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="39753-119">Tras finalizar y devuelve el símbolo del sistema de toohello instalación, cierre la ventana de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="39753-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="39753-120">Inicie un nuevo símbolo del sistema (cmd) desde el menú de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="39753-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="39753-121">Hola prueba instalación Ruby `ruby -v` versión de hello toosee instalada.</span><span class="sxs-lookup"><span data-stu-id="39753-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="39753-122">Probar la instalación de indicador de hello `gem -v` versión de hello toosee instalada.</span><span class="sxs-lookup"><span data-stu-id="39753-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="39753-123">Generar el módulo de PostgreSQL Hola para Ruby con indicador mediante la ejecución de comando hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="39753-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="39753-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="39753-124">MacOS</span></span>
- <span data-ttu-id="39753-125">Instalar Ruby con Homebrew mediante la ejecución de comando hello `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="39753-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="39753-126">Para obtener más opciones de instalación, vea Hola Ruby [documentación de la instalación](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="39753-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="39753-127">Hola prueba instalación Ruby `ruby -v` versión de hello toosee instalada.</span><span class="sxs-lookup"><span data-stu-id="39753-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="39753-128">Probar la instalación de indicador de hello `gem -v` versión de hello toosee instalada.</span><span class="sxs-lookup"><span data-stu-id="39753-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="39753-129">Generar el módulo de PostgreSQL Hola para Ruby con indicador mediante la ejecución de comando hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="39753-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="39753-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="39753-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="39753-131">Instale Ruby ejecutando el comando de hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="39753-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="39753-132">Para obtener más opciones de instalación, vea Hola Ruby [documentación de la instalación](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="39753-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="39753-133">Hola prueba instalación Ruby `ruby -v` versión de hello toosee instalada.</span><span class="sxs-lookup"><span data-stu-id="39753-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="39753-134">Instalar las actualizaciones más recientes de Hola para indicador mediante la ejecución de comando hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="39753-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="39753-135">Probar la instalación de indicador de hello `gem -v` versión de hello toosee instalada.</span><span class="sxs-lookup"><span data-stu-id="39753-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="39753-136">Instalar gcc hello, marca y otras herramientas de compilación mediante la ejecución de comando hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="39753-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="39753-137">Instalar bibliotecas de PostgreSQL hello mediante la ejecución de comando hello `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="39753-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="39753-138">Generar el módulo de hello pg Ruby con indicador mediante la ejecución de comando hello `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="39753-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="39753-139">Ejecución del código Ruby</span><span class="sxs-lookup"><span data-stu-id="39753-139">Run Ruby code</span></span> 
- <span data-ttu-id="39753-140">Guardar el código de hello en un archivo de texto y guardar archivo hello en una carpeta del proyecto con RB de extensión de archivo, como `C:\rubypostgres\read.rb` o`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="39753-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="39753-141">código de hello toorun, inicie el símbolo del sistema de Hola o el shell de bash.</span><span class="sxs-lookup"><span data-stu-id="39753-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="39753-142">Cambie el directorio a la carpeta de proyecto `cd rubypostgres`, a continuación, escriba el comando de hello `ruby read.rb` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="39753-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="39753-143">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="39753-143">Get connection information</span></span>
<span data-ttu-id="39753-144">Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="39753-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="39753-145">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="39753-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="39753-146">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="39753-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="39753-147">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="39753-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="39753-148">Haga clic en el nombre del servidor de hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="39753-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="39753-149">Servidor de hello seleccione **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="39753-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="39753-150">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="39753-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="39753-151">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="39753-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="39753-152">Si olvida su información de inicio de sesión de servidor, vaya a toohello **Introducción** nombre de inicio de sesión del Administrador de servidor de página tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="39753-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="39753-153">Si es necesario, Hola de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="39753-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="39753-154">Conexión y creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="39753-154">Connect and create a table</span></span>
<span data-ttu-id="39753-155">Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL, seguido de **INSERT INTO** tooadd filas de las instrucciones de SQL en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="39753-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="39753-156">código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="39753-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="39753-157">A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello, CREATE TABLE, comandos DROP y INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="39753-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="39753-158">Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase.</span><span class="sxs-lookup"><span data-stu-id="39753-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="39753-159">A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.</span><span class="sxs-lookup"><span data-stu-id="39753-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="39753-160">Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="39753-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a><span data-ttu-id="39753-161">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="39753-161">Read data</span></span>
<span data-ttu-id="39753-162">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="39753-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="39753-163">código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="39753-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="39753-164">A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hola del comando SELECT, mantener Hola de resultados en un conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="39753-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="39753-165">Hello colección de conjuntos de resultados se recorre en iteración utilizando hello `resultSet.each do` bucles, conservando los valores de fila actuales de Hola Hola `row` variable.</span><span class="sxs-lookup"><span data-stu-id="39753-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="39753-166">Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase.</span><span class="sxs-lookup"><span data-stu-id="39753-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="39753-167">A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.</span><span class="sxs-lookup"><span data-stu-id="39753-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="39753-168">Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="39753-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a><span data-ttu-id="39753-169">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="39753-169">Update data</span></span>
<span data-ttu-id="39753-170">Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="39753-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="39753-171">código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="39753-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="39753-172">A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hola comando de actualización.</span><span class="sxs-lookup"><span data-stu-id="39753-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="39753-173">Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase.</span><span class="sxs-lookup"><span data-stu-id="39753-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="39753-174">A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.</span><span class="sxs-lookup"><span data-stu-id="39753-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="39753-175">Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="39753-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="39753-176">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="39753-176">Delete data</span></span>
<span data-ttu-id="39753-177">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="39753-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="39753-178">código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="39753-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="39753-179">A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hola comando de actualización.</span><span class="sxs-lookup"><span data-stu-id="39753-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="39753-180">Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase.</span><span class="sxs-lookup"><span data-stu-id="39753-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="39753-181">A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.</span><span class="sxs-lookup"><span data-stu-id="39753-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="39753-182">Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="39753-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="39753-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39753-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="39753-184">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="39753-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
