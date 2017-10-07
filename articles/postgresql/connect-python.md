---
title: Conectar tooAzure base de datos de PostgreSQL desde Python | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo de código de Python que puede usar tooconnect y consultar los datos de la base de datos PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a>Base de datos de Azure para PostgreSQL: uso de Python tooconnect y consultar datos
Este tutorial rápido muestra cómo toouse [Python](https://python.org) tooconnect tooan base de datos de Azure para PostgreSQL. También se muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola de macOS y Ubuntu Linux, plataformas de Windows. pasos de Hello en este artículo se supone que está familiarizado con el desarrollo con Python y son tooworking nueva con la base de datos de Azure para PostgreSQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Creación de la base de datos: Azure Portal](quickstart-create-server-database-portal.md)
- [Creación de la base de datos: CLI](quickstart-create-server-database-azure-cli.md)

También necesita lo siguiente:
- Tener instalado [Python](https://www.python.org/downloads/)
- Tener instalado el paquete [pip](https://pip.pypa.io/en/stable/installing/) (pip ya está instalado si trabaja con binarios de Python 2 >=2.7.9 o Python 3 >=3.4 descargados de [python.org](https://python.org).

## <a name="install-hello-python-connection-libraries-for-postgresql"></a>Instalar bibliotecas de conexiones de hello Python para PostgreSQL
Instalar hello [psycopg2](http://initd.org/psycopg/docs/install.html) paquete, lo que permite la base de datos de hello tooconnect y consulta. es psycopg2 [disponible en PyPI](https://pypi.python.org/pypi/psycopg2/) en forma de Hola de [rueda](http://pythonwheels.com/) paquetes para plataformas más comunes de hello (Linux, OSX, Windows). Use pip instalar versión binaria de hello tooget del módulo de hello incluyendo todas las dependencias de Hola.

1. En su propio equipo, inicie una interfaz de la línea de comandos:
    - En Linux, inicie el shell de Bash Hola.
    - En Mac OS, inicie Hola Terminal.
    - En Windows, inicie Hola símbolo del sistema desde el menú Inicio Hola.
2. Asegúrese de que está utilizando la versión más reciente de hello del pip al ejecutar un comando como:
    ```cmd
    pip install -U pip
    ```

3. Ejecute hello después el paquete de comando tooinstall Hola psycopg2:
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque **mypgserver 20170401** (servidor de Hola que acaba de crear).
3. Haga clic en el nombre del servidor de hello **mypgserver 20170401**.
4. Servidor de hello seleccione **información general sobre** página y, a continuación, tome nota del programa Hola a **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-python/1-connection-string.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="how-toorun-python-code"></a>¿Cómo toorun código Python
Este tema contiene cuatro ejemplos de código en total, cada uno de los cuales realiza una función específica. Hello las instrucciones siguientes indican cómo toocreate un archivo de texto, insertar un bloque de código y, a continuación, guardar archivo hello para que se pueda ejecutar más adelante. Ser seguro toocreate cuatro archivos independientes, uno para cada bloque de código.

- Con su editor de texto favorito, cree un nuevo archivo.
- Copie y pegue uno de los ejemplos de código de hello en hello las secciones siguientes en el archivo de texto hello. Reemplace hello **host**, **dbname**, **usuario**, y **contraseña** parámetros con valores de hello que especificó cuando creó Hola servidor y base de datos.
- Guarde el archivo de hello con la extensión de hello .py (por ejemplo, postgres.py) en la carpeta del proyecto. Si está ejecutando sistema operativo Windows hello, ser seguro tooselect codificación UTF-8 al guardar el archivo hello. 
- Inicie el shell de línea de comandos o intensiva de errores de hello y, a continuación, cambiar carpeta del proyecto de hello directory tooyour, por ejemplo `cd postgres`.
-  código de hello toorun, Hola de tipo seguido por nombre de archivo de hello, por ejemplo de comando de Python `Python postgres.py`.

> [!NOTE]
> A partir de la versión 3 de Python, puede ver el error de hello `SyntaxError: Missing parentheses in call too'print'` cuando se ejecuta después de los bloques de código de hello. Si esto sucede, reemplace cada llamadas (comando) toohello `print "string"` con una llamada de función con paréntesis, como `print("string")`.

## <a name="connect-create-table-and-insert-data"></a>Conexión, creación de una tabla e inserción de datos
Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) funcionando con **insertar** instrucción SQL. Hola [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL. Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

Después de hello código se ejecuta correctamente, salida de hello aparece como sigue:

![Salida de línea de comandos](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a>Lectura de datos
Datos de Hola de tooread insertadas utilizando la sintaxis de código siguiente Hola de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionando con **seleccione** instrucción SQL. Esta función acepta una consulta y se devuelve un conjunto de resultados que puede iterar sobre usando Hola de [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall). Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a>Actualización de datos
Siguiente de Hola de uso de código fila de inventario de hello tooupdate que anteriormente se hubiera insertado utilizando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionando con **actualización** instrucción SQL. Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a>Eliminación de datos
Siguiente de Hola de uso de código toodelete un artículo de inventario que se hubiera insertado previamente mediante [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionando con **eliminar** instrucción SQL. Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./howto-migrate-using-export-and-import.md)
