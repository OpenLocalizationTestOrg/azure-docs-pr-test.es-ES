---
title: Conectar tooAzure base de datos de MySQL de Python | Documentos de Microsoft
description: "Este tutorial rápido proporciona que ejemplos que puede utilizar tooconnect y consultar datos de base de datos de Azure para MySQL de código de Python varias."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Base de datos de Azure para MySQL: uso de Python tooconnect y consultar datos
Este tutorial rápido muestra cómo toouse [Python](https://python.org) tooconnect tooan base de datos de Azure para MySQL. Usa tooquery de instrucciones SQL, insert, update y delete datos en base de datos de hello en plataformas Windows, Mac OS y Ubuntu Linux. pasos de Hello en este artículo se supone que está familiarizado con el desarrollo con Python y son tooworking nueva con la base de datos de Azure para MySQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

## <a name="install-python-and-hello-mysql-connector"></a>Instalar Python y Hola conector MySQL
Instalar [Python](https://www.python.org/downloads/) hello y [conector MySQL de Python](https://dev.mysql.com/downloads/connector/python/) en su propio equipo. Dependiendo de la plataforma, siga los pasos de hello:

### <a name="windows"></a>Windows
1. Descargue e instale Python 2.7 desde [python.org](https://www.python.org/downloads/windows/). 
2. Comprobar instalación de Python Hola iniciando Hola símbolo del sistema. Ejecute el comando de hello `C:\python27\python.exe -V` con número de versión de Hola mayúsculas V conmutador toosee Hola.
3. Instalar el conector de Python de Hola para MySQL desde [mysql.com](https://dev.mysql.com/downloads/connector/python/) versión tooyour correspondiente de Python.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Linux (Ubuntu), Python normalmente se instala como parte de la instalación predeterminada de Hola.
2. Compruebe la instalación de Python de hello iniciando el shell de bash Hola. Ejecute el comando de hello `python -V` con número de versión de Hola mayúsculas V conmutador toosee Hola.
3. Comprobar instalación de PIP de hello ejecutando hello `pip show pip -V` número de versión de hello toosee de comandos. 
4. PIP puede estar incluido en algunas versiones de Python. Si no está instalado el PIP, puede instalar Hola [PIP] (https://pip.pypa.io/en/stable/installing/) paquete, mediante la ejecución de comando `sudo apt-get install python-pip`.
5. Actualización PIP toohello versión más reciente, mediante la ejecución de hello `pip install -U pip` comando.
6. Instale el conector de MySQL de Hola para Python y sus dependencias mediante Hola PIP comando:

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. En Mac OS, Python normalmente se instala como parte de la instalación del SO predeterminado Hola.
2. Compruebe la instalación de Python de hello iniciando el shell de bash Hola. Ejecute el comando de hello `python -V` con número de versión de Hola mayúsculas V conmutador toosee Hola.
3. Comprobar instalación de PIP de hello ejecutando hello `pip show pip -V` número de versión de hello toosee de comandos.
4. PIP puede estar incluido en algunas versiones de Python. Si no está instalado el PIP, puede instalar hello [PIP](https://pip.pypa.io/en/stable/installing/) paquete.
5. Actualización PIP toohello versión más reciente, mediante la ejecución de hello `pip install -U pip` comando.
6. Instale el conector de MySQL de Hola para Python y sus dependencias mediante Hola PIP comando:

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque servidor hello plegado, como **myserver4demo**.
3. Haga clic en el nombre del servidor de hello **myserver4demo**.
4. Servidor de hello seleccione **propiedades** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-python/1_server-properties-name-login.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.
   

## <a name="run-python-code"></a>Ejecución de código de Python
- Pegue el código de hello en un archivo de texto y guarde el archivo hello en una carpeta del proyecto con .py de extensión de archivo, como C:\pythonmysql\createtable.py o /home/username/pythonmysql/createtable.py
- código de hello toorun, inicie el símbolo del sistema de Hola o el shell de bash. Cambie el directorio a la carpeta de proyecto `cd pythonmysql`. A continuación, escriba el comando de python de hello seguido por el nombre de archivo de hello `python createtable.py` aplicación de hello toorun. En el sistema operativo Windows hello, si no se encuentra python.exe, puede proporcionar toohello de ruta de acceso completa de hello ejecutable o agregar la ruta de acceso de Python de hello en la variable de entorno path de Hola. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Conexión, creación de una tabla e inserción de datos
Siguiente Hola de uso codificar tooconnect toohello server, cree una tabla y cargar datos de hello mediante un **insertar** instrucción SQL. 

En el código de hello, se importa la biblioteca de mysql.connector Hola. Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola. código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la consulta SQL de hello en base de datos MySQL. 

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. 

En el código de hello, se importa la biblioteca de mysql.connector Hola. Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola. código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la instrucción de SQL de hello en base de datos MySQL. las filas de datos de Hola se leen con hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) método. conjunto de resultados Hello se mantiene una en una fila de la colección y una para iterador es tooloop utilizado en filas de Hola.

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL. 

En el código de hello, se importa la biblioteca de mysql.connector Hola.  Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola. código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la instrucción de SQL de hello en base de datos MySQL. 

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y eliminar los datos mediante un **eliminar** instrucción SQL. 

En el código de hello, se importa la biblioteca de mysql.connector Hola.  Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola. código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la consulta SQL de hello en base de datos MySQL. 

Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./concepts-migrate-import-export.md)
