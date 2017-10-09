---
title: Conectar tooAzure base de datos de MySQL con Ruby | Documentos de Microsoft
description: "Este tutorial rápido proporciona varios ejemplos de código Ruby puede usar tooconnect y consultar los datos de la base de datos MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Base de datos de Azure para MySQL: Use Ruby tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos de MySQL utilizando un [Ruby](https://www.ruby-lang.org) hello y aplicación [mysql2](https://rubygems.org/gems/mysql2) indicador entre plataformas de Windows, Ubuntu Linux y Mac. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. En este artículo se da por supuesto que está familiarizado con el desarrollo mediante Ruby, pero que se tooworking nueva con la base de datos de Azure para MySQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

## <a name="install-ruby"></a>Instalación de Ruby
Instalar Ruby, la biblioteca de MySQL2 hello e indicador en su propio equipo. 

### <a name="windows"></a>Windows
1. Descargue e instale la versión de Hola 2.3 de [Ruby](http://rubyinstaller.org/downloads/).
2. Inicie un nuevo símbolo del sistema (cmd) desde el menú de inicio de Hola.
3. Cambie el directorio en hello Ruby directorio para la versión 2.3. `cd c:\Ruby23-x64\bin`
4. Hola prueba Ruby instalación mediante la ejecución de comando hello `ruby -v` versión de hello toosee instalada.
5. Probar la instalación de indicador de hello mediante la ejecución de comando hello `gem -v` versión de hello toosee instalada.
6. Generar el módulo de hello Mysql2 para Ruby con indicador mediante la ejecución de comando hello `gem install mysql2`.

### <a name="macos"></a>MacOS
1. Instalar Ruby con Homebrew mediante la ejecución de comando hello `brew install ruby`. Para obtener más opciones de instalación, vea Hola Ruby [documentación de la instalación](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Hola prueba Ruby instalación mediante la ejecución de comando hello `ruby -v` versión de hello toosee instalada.
3. Probar la instalación de indicador de hello mediante la ejecución de comando hello `gem -v` versión de hello toosee instalada.
4. Generar el módulo de hello Mysql2 para Ruby con indicador mediante la ejecución de comando hello `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Instale Ruby ejecutando el comando de hello `sudo apt-get install ruby-full`. Para obtener más opciones de instalación, vea Hola Ruby [documentación de la instalación](https://www.ruby-lang.org/en/documentation/installation/).
2. Hola prueba Ruby instalación mediante la ejecución de comando hello `ruby -v` versión de hello toosee instalada.
3. Instalar las actualizaciones más recientes de Hola para indicador mediante la ejecución de comando hello `sudo gem update --system`.
4. Probar la instalación de indicador de hello mediante la ejecución de comando hello `gem -v` versión de hello toosee instalada.
5. Instalar gcc hello, marca y otras herramientas de compilación mediante la ejecución de comando hello `sudo apt-get install build-essential`.
6. Instalar bibliotecas de desarrollador de cliente de MySQL de hello mediante la ejecución de comando hello `sudo apt-get install libmysqlclient-dev`.
7. Generar el módulo de mysql2 Hola para Ruby con indicador mediante la ejecución de comando hello `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque servidor hello plegado, como **myserver4demo**.
3. Haga clic en el nombre del servidor de hello **myserver4demo**.
4. Servidor de hello seleccione **propiedades** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-ruby/1_server-properties-name-login.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="run-ruby-code"></a>Ejecución del código Ruby 
1. Pegue Hola Ruby código de las secciones de Hola a continuación en archivos de texto y guardar archivos de hello en una carpeta del proyecto con RB de extensión de archivo, como `C:\rubymysql\createtable.rb` o `/home/username/rubymysql/createtable.rb`.
2. código de hello toorun, inicie el símbolo del sistema de Hola o el shell de bash. Cambie el directorio a la carpeta de proyecto `cd rubymysql`.
3. A continuación, escriba el comando hello ruby seguida por nombre de archivo de hello, como `ruby createtable.rb` aplicación de hello toorun.
4. En el sistema operativo Windows hello, si la aplicación hello ruby no está en la variable de entorno path, puede necesita toouse Hola ruta de acceso completa toolaunch Hola nodo aplicación, como`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Conexión y creación de una tabla
Código tooconnect siguiente de Hola de uso y crear una tabla mediante **CREATE TABLE** instrucción SQL, seguido de **INSERT INTO** tooadd filas de las instrucciones de SQL en la tabla de Hola.

código de Hello usa un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) clase .new() método tooconnect tooAzure base de datos de MySQL. A continuación, llama el método [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) varias veces toorun hello, CREATE TABLE, comandos DROP y INSERT INTO. A continuación, llama el método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `username`, y `password` cadenas con sus propios valores. 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. 

código de Hello usa un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) clase .new() método tooconnect tooAzure base de datos de MySQL. A continuación, llama el método [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) comandos SELECT de toorun Hola. A continuación, llama el método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `username`, y `password` cadenas con sus propios valores. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.

código de Hello usa un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) clase .new() método tooconnect tooAzure base de datos de MySQL. A continuación, llama el método [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) comandos de actualización de toorun Hola. A continuación, llama el método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `username`, y `password` cadenas con sus propios valores. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. 

código de Hello usa un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) clase .new() método tooconnect tooAzure base de datos de MySQL. A continuación, llama el método [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) comandos DELETE de toorun Hola. A continuación, llama el método [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) conexión de hello tooclose antes de finalizar.

Reemplace hello `host`, `database`, `username`, y `password` cadenas con sus propios valores. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./concepts-migrate-import-export.md)
