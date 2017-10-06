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
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Base de datos de Azure para PostgreSQL: Use Ruby tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure base de datos PostgreSQL utilizando un [Ruby](https://www.ruby-lang.org) aplicación. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. En este artículo se da por supuesto que está familiarizado con el desarrollo mediante Ruby, pero que se tooworking nueva con la base de datos de Azure para PostgreSQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Creación de la base de datos: Azure Portal](quickstart-create-server-database-portal.md)
- [Creación de la base de datos: CLI de Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Instalación de Ruby
Instale Ruby en su propia máquina. 

### <a name="windows"></a>Windows
- Descarga e instale Hola versión más reciente de [Ruby](http://rubyinstaller.org/downloads/).
- En hello, finalizar la pantalla del instalador MSI de hello, casilla Hola que dice "ejecución 'ridk instalar' tooinstall MSYS2 y cadena de herramientas de desarrollo". A continuación, haga clic en **finalizar** instalador de toolaunch Hola siguiente.
- se inicia el instalador de RubyInstaller2 para Windows Hello. Tipo de actualización de repositorio de hello MSYS2 tooinstall 2. Tras finalizar y devuelve el símbolo del sistema de toohello instalación, cierre la ventana de comandos de Hola.
- Inicie un nuevo símbolo del sistema (cmd) desde el menú de inicio de Hola.
- Hola prueba instalación Ruby `ruby -v` versión de hello toosee instalada.
- Probar la instalación de indicador de hello `gem -v` versión de hello toosee instalada.
- Generar el módulo de PostgreSQL Hola para Ruby con indicador mediante la ejecución de comando hello `gem install pg`.

### <a name="macos"></a>MacOS
- Instalar Ruby con Homebrew mediante la ejecución de comando hello `brew install ruby`. Para obtener más opciones de instalación, vea Hola Ruby [documentación de la instalación](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- Hola prueba instalación Ruby `ruby -v` versión de hello toosee instalada.
- Probar la instalación de indicador de hello `gem -v` versión de hello toosee instalada.
- Generar el módulo de PostgreSQL Hola para Ruby con indicador mediante la ejecución de comando hello `gem install pg`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Instale Ruby ejecutando el comando de hello `sudo apt-get install ruby-full`. Para obtener más opciones de instalación, vea Hola Ruby [documentación de la instalación](https://www.ruby-lang.org/en/documentation/installation/).
- Hola prueba instalación Ruby `ruby -v` versión de hello toosee instalada.
- Instalar las actualizaciones más recientes de Hola para indicador mediante la ejecución de comando hello `sudo gem update --system`.
- Probar la instalación de indicador de hello `gem -v` versión de hello toosee instalada.
- Instalar gcc hello, marca y otras herramientas de compilación mediante la ejecución de comando hello `sudo apt-get install build-essential`.
- Instalar bibliotecas de PostgreSQL hello mediante la ejecución de comando hello `sudo apt-get install libpq-dev`.
- Generar el módulo de hello pg Ruby con indicador mediante la ejecución de comando hello `sudo gem install pg`.

## <a name="run-ruby-code"></a>Ejecución del código Ruby 
- Guardar el código de hello en un archivo de texto y guardar archivo hello en una carpeta del proyecto con RB de extensión de archivo, como `C:\rubypostgres\read.rb` o`/home/username/rubypostgres/read.rb`
- código de hello toorun, inicie el símbolo del sistema de Hola o el shell de bash. Cambie el directorio a la carpeta de proyecto `cd rubypostgres`, a continuación, escriba el comando de hello `ruby read.rb` aplicación de hello toorun.

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.
3. Haga clic en el nombre del servidor de hello **mypgserver 20170401**.
4. Servidor de hello seleccione **Introducción** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-ruby/1-connection-string.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **Introducción** nombre de inicio de sesión del Administrador de servidor de página tooview Hola. Si es necesario, Hola de restablecimiento de contraseña.

## <a name="connect-and-create-a-table"></a>Conexión y creación de una tabla
Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL, seguido de **INSERT INTO** tooadd filas de las instrucciones de SQL en la tabla de Hola.

código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL. A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello, CREATE TABLE, comandos DROP y INSERT INTO. Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase. A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores. 
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

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. 

código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL. A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hola del comando SELECT, mantener Hola de resultados en un conjunto de resultados. Hello colección de conjuntos de resultados se recorre en iteración utilizando hello `resultSet.each do` bucles, conservando los valores de fila actuales de Hola Hola `row` variable. Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase. A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores. 

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

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.

código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL. A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hola comando de actualización. Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase. A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores. 

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


## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. 

código de Hello usa un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objeto con el constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de datos de PostgreSQL. A continuación, llama el método [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun Hola comando de actualización. Hello código comprueba si hay errores mediante hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) clase. A continuación, llama el método [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `user`, y `password` cadenas con sus propios valores. 

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

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./howto-migrate-using-export-and-import.md)
