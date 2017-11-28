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
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="0747d-103">Base de datos de Azure para PostgreSQL: uso de Python tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="0747d-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="0747d-104">Este tutorial rápido muestra cómo toouse [Python](https://python.org) tooconnect tooan base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0747d-105">También se muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola de macOS y Ubuntu Linux, plataformas de Windows.</span><span class="sxs-lookup"><span data-stu-id="0747d-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="0747d-106">pasos de Hello en este artículo se supone que está familiarizado con el desarrollo con Python y son tooworking nueva con la base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0747d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0747d-107">Prerequisites</span></span>
<span data-ttu-id="0747d-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="0747d-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0747d-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0747d-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="0747d-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="0747d-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="0747d-111">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0747d-111">You also need:</span></span>
- <span data-ttu-id="0747d-112">Tener instalado [Python](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="0747d-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="0747d-113">Tener instalado el paquete [pip](https://pip.pypa.io/en/stable/installing/) (pip ya está instalado si trabaja con binarios de Python 2 >=2.7.9 o Python 3 >=3.4 descargados de [python.org](https://python.org).</span><span class="sxs-lookup"><span data-stu-id="0747d-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="0747d-114">Instalar bibliotecas de conexiones de hello Python para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0747d-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="0747d-115">Instalar hello [psycopg2](http://initd.org/psycopg/docs/install.html) paquete, lo que permite la base de datos de hello tooconnect y consulta.</span><span class="sxs-lookup"><span data-stu-id="0747d-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="0747d-116">es psycopg2 [disponible en PyPI](https://pypi.python.org/pypi/psycopg2/) en forma de Hola de [rueda](http://pythonwheels.com/) paquetes para plataformas más comunes de hello (Linux, OSX, Windows).</span><span class="sxs-lookup"><span data-stu-id="0747d-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="0747d-117">Use pip instalar versión binaria de hello tooget del módulo de hello incluyendo todas las dependencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="0747d-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="0747d-118">En su propio equipo, inicie una interfaz de la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="0747d-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="0747d-119">En Linux, inicie el shell de Bash Hola.</span><span class="sxs-lookup"><span data-stu-id="0747d-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="0747d-120">En Mac OS, inicie Hola Terminal.</span><span class="sxs-lookup"><span data-stu-id="0747d-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="0747d-121">En Windows, inicie Hola símbolo del sistema desde el menú Inicio Hola.</span><span class="sxs-lookup"><span data-stu-id="0747d-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="0747d-122">Asegúrese de que está utilizando la versión más reciente de hello del pip al ejecutar un comando como:</span><span class="sxs-lookup"><span data-stu-id="0747d-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="0747d-123">Ejecute hello después el paquete de comando tooinstall Hola psycopg2:</span><span class="sxs-lookup"><span data-stu-id="0747d-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="0747d-124">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="0747d-124">Get connection information</span></span>
<span data-ttu-id="0747d-125">Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0747d-126">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="0747d-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0747d-127">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0747d-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0747d-128">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque **mypgserver 20170401** (servidor de Hola que acaba de crear).</span><span class="sxs-lookup"><span data-stu-id="0747d-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="0747d-129">Haga clic en el nombre del servidor de hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="0747d-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="0747d-130">Servidor de hello seleccione **información general sobre** página y, a continuación, tome nota del programa Hola a **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="0747d-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0747d-131">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="0747d-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="0747d-132">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="0747d-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="0747d-133">¿Cómo toorun código Python</span><span class="sxs-lookup"><span data-stu-id="0747d-133">How toorun Python code</span></span>
<span data-ttu-id="0747d-134">Este tema contiene cuatro ejemplos de código en total, cada uno de los cuales realiza una función específica.</span><span class="sxs-lookup"><span data-stu-id="0747d-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="0747d-135">Hello las instrucciones siguientes indican cómo toocreate un archivo de texto, insertar un bloque de código y, a continuación, guardar archivo hello para que se pueda ejecutar más adelante.</span><span class="sxs-lookup"><span data-stu-id="0747d-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="0747d-136">Ser seguro toocreate cuatro archivos independientes, uno para cada bloque de código.</span><span class="sxs-lookup"><span data-stu-id="0747d-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="0747d-137">Con su editor de texto favorito, cree un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="0747d-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="0747d-138">Copie y pegue uno de los ejemplos de código de hello en hello las secciones siguientes en el archivo de texto hello.</span><span class="sxs-lookup"><span data-stu-id="0747d-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="0747d-139">Reemplace hello **host**, **dbname**, **usuario**, y **contraseña** parámetros con valores de hello que especificó cuando creó Hola servidor y base de datos.</span><span class="sxs-lookup"><span data-stu-id="0747d-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="0747d-140">Guarde el archivo de hello con la extensión de hello .py (por ejemplo, postgres.py) en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="0747d-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="0747d-141">Si está ejecutando sistema operativo Windows hello, ser seguro tooselect codificación UTF-8 al guardar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="0747d-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="0747d-142">Inicie el shell de línea de comandos o intensiva de errores de hello y, a continuación, cambiar carpeta del proyecto de hello directory tooyour, por ejemplo `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="0747d-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="0747d-143">código de hello toorun, Hola de tipo seguido por nombre de archivo de hello, por ejemplo de comando de Python `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="0747d-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="0747d-144">A partir de la versión 3 de Python, puede ver el error de hello `SyntaxError: Missing parentheses in call too'print'` cuando se ejecuta después de los bloques de código de hello.</span><span class="sxs-lookup"><span data-stu-id="0747d-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="0747d-145">Si esto sucede, reemplace cada llamadas (comando) toohello `print "string"` con una llamada de función con paréntesis, como `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="0747d-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="0747d-146">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="0747d-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="0747d-147">Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) funcionando con **insertar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="0747d-148">Hola [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) función es consulta SQL hello tooexecute usado en la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="0747d-149">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0747d-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

<span data-ttu-id="0747d-150">Después de hello código se ejecuta correctamente, salida de hello aparece como sigue:</span><span class="sxs-lookup"><span data-stu-id="0747d-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Salida de línea de comandos](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="0747d-152">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="0747d-152">Read data</span></span>
<span data-ttu-id="0747d-153">Datos de Hola de tooread insertadas utilizando la sintaxis de código siguiente Hola de uso [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionando con **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="0747d-154">Esta función acepta una consulta y se devuelve un conjunto de resultados que puede iterar sobre usando Hola de [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="0747d-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="0747d-155">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0747d-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="0747d-156">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="0747d-156">Update data</span></span>
<span data-ttu-id="0747d-157">Siguiente de Hola de uso de código fila de inventario de hello tooupdate que anteriormente se hubiera insertado utilizando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionando con **actualización** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="0747d-158">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0747d-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="0747d-159">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="0747d-159">Delete data</span></span>
<span data-ttu-id="0747d-160">Siguiente de Hola de uso de código toodelete un artículo de inventario que se hubiera insertado previamente mediante [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funcionando con **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="0747d-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="0747d-161">Reemplazar host hello, dbname, usuario y contraseña parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0747d-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0747d-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0747d-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0747d-163">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="0747d-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
