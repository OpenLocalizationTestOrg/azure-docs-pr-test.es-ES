---
title: "Conexión a Azure Database for PostgreSQL desde Python | Microsoft Docs"
description: "En este tutorial rápido se proporciona un ejemplo de código de Python que puede usar para conectarse a Azure Database for PostgreSQL y consultar datos en este servicio."
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
ms.openlocfilehash: d682d94143fb9fd5e2c2a578c3cb0dcfa101462c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-python-to-connect-and-query-data"></a><span data-ttu-id="8b2a7-103">Azure Database for PostgreSQL: uso de Python para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="8b2a7-103">Azure Database for PostgreSQL: Use Python to connect and query data</span></span>
<span data-ttu-id="8b2a7-104">En este tutorial de inicio rápido se muestra cómo usar [Python](https://python.org) para conectarse a una instancia de Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8b2a7-105">También se muestra cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos en plataformas macOS, Ubuntu Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-105">It also demonstrates how to use SQL statements to query, insert, update, and delete data in the database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="8b2a7-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante Python, pero que nunca ha trabajado con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b2a7-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8b2a7-107">Prerequisites</span></span>
<span data-ttu-id="8b2a7-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="8b2a7-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="8b2a7-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8b2a7-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="8b2a7-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="8b2a7-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="8b2a7-111">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8b2a7-111">You also need:</span></span>
- <span data-ttu-id="8b2a7-112">Tener instalado [Python](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="8b2a7-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="8b2a7-113">Tener instalado el paquete [pip](https://pip.pypa.io/en/stable/installing/) (pip ya está instalado si trabaja con binarios de Python 2 >=2.7.9 o Python 3 >=3.4 descargados de [python.org](https://python.org).</span><span class="sxs-lookup"><span data-stu-id="8b2a7-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-the-python-connection-libraries-for-postgresql"></a><span data-ttu-id="8b2a7-114">Instalación de las bibliotecas de conexiones de Python para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8b2a7-114">Install the Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="8b2a7-115">Instale el paquete [psycopg2](http://initd.org/psycopg/docs/install.html), que le permite conectarse y consultar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-115">Install the [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you to connect and query the database.</span></span> <span data-ttu-id="8b2a7-116">psycopg2 está [disponible en PyPI](https://pypi.python.org/pypi/psycopg2/) en forma de paquetes [wheel](http://pythonwheels.com/) para la mayoría de las plataformas (Linux, OSX, Windows).</span><span class="sxs-lookup"><span data-stu-id="8b2a7-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in the form of [wheel](http://pythonwheels.com/) packages for the most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="8b2a7-117">Use pip install para obtener la versión binaria del módulo, incluidas todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-117">Use pip install to get the binary version of the module including all the dependencies.</span></span>

1. <span data-ttu-id="8b2a7-118">En su propio equipo, inicie una interfaz de la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="8b2a7-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="8b2a7-119">En Linux, inicie el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-119">On Linux, launch the Bash shell.</span></span>
    - <span data-ttu-id="8b2a7-120">En macOS, inicie Terminal.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-120">On macOS, launch the Terminal.</span></span>
    - <span data-ttu-id="8b2a7-121">En Windows, inicie el símbolo del sistema desde el menú Inicio.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-121">On Windows, launch the Command Prompt from the Start Menu.</span></span>
2. <span data-ttu-id="8b2a7-122">Asegúrese de que está usando la versión más reciente de pip; para ello, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="8b2a7-122">Ensure that you are using the most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="8b2a7-123">Ejecute el comando siguiente para instalar el paquete de psycopg2:</span><span class="sxs-lookup"><span data-stu-id="8b2a7-123">Run the following command to install the psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="8b2a7-124">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="8b2a7-124">Get connection information</span></span>
<span data-ttu-id="8b2a7-125">Obtenga la información de conexión necesaria para conectarse a Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-125">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8b2a7-126">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-126">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="8b2a7-127">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8b2a7-127">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8b2a7-128">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque **mypgserver-20170401** (el servidor que acaba de crear).</span><span class="sxs-lookup"><span data-stu-id="8b2a7-128">From the left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (the server you just created).</span></span>
3. <span data-ttu-id="8b2a7-129">Haga clic en el nombre del servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-129">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="8b2a7-130">Seleccione la página **Información general** del servidor, anote el **nombre del servidor** y el **nombre de inicio de sesión del administrador del servidor**.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-130">Select the server's **Overview** page, and then make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="8b2a7-131">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="8b2a7-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="8b2a7-132">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-132">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="how-to-run-python-code"></a><span data-ttu-id="8b2a7-133">Ejecución de código Python</span><span class="sxs-lookup"><span data-stu-id="8b2a7-133">How to run Python code</span></span>
<span data-ttu-id="8b2a7-134">Este tema contiene cuatro ejemplos de código en total, cada uno de los cuales realiza una función específica.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="8b2a7-135">Las siguientes instrucciones indican cómo crear un archivo de texto, insertar un bloque de código y luego guardar el archivo para que se pueda ejecutar más adelante.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-135">The following instructions indicate how to create a text file, insert a code block, and then save the file so that you can run it later.</span></span> <span data-ttu-id="8b2a7-136">No olvide crear cuatro archivos diferentes, uno para cada bloque de código.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-136">Be sure to create four separate files, one for each code block.</span></span>

- <span data-ttu-id="8b2a7-137">Con su editor de texto favorito, cree un nuevo archivo.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="8b2a7-138">Copie y pegue uno de los ejemplos de código en las secciones siguientes del archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-138">Copy and paste one of the code samples in the following sections into the text file.</span></span> <span data-ttu-id="8b2a7-139">Reemplace los parámetros **host**, **dbname**, **user** y **password** por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-139">Replace the **host**, **dbname**, **user**, and **password** parameters with the values that you specified when you created the server and database.</span></span>
- <span data-ttu-id="8b2a7-140">Guarde el archivo con la extensión .py (por ejemplo, postgres.py) en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-140">Save the file with the .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="8b2a7-141">Si va a ejecutar el sistema operativo Windows, asegúrese de seleccionar la codificación UTF-8 cuando guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-141">If you are running the Windows OS, be sure to select UTF-8 encoding when saving the file.</span></span> 
- <span data-ttu-id="8b2a7-142">Inicie el símbolo del sistema o el shell de Bash y luego cambie el directorio a la carpeta del proyecto, por ejemplo `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-142">Launch the Command Prompt or Bash shell and then change the directory to your project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="8b2a7-143">Para ejecutar el código, escriba el comando de Python seguido del nombre de archivo, por ejemplo `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-143">To run the code, type the Python command followed by the file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="8b2a7-144">A partir de la versión 3 de Python, es posible que al ejecutar los bloques de código siguientes vea el error `SyntaxError: Missing parentheses in call to 'print'`.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-144">Starting in Python version 3, you may see the error `SyntaxError: Missing parentheses in call to 'print'` when running the following code blocks.</span></span> <span data-ttu-id="8b2a7-145">Si esto sucede, reemplace cada llamada al comando `print "string"` por una llamada de función con paréntesis, como `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-145">If that happens, replace each call to the command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="8b2a7-146">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="8b2a7-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="8b2a7-147">Use el código siguiente para conectarse y cargar los datos mediante la función [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) con la instrucción SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-147">Use the following code to connect and load the data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="8b2a7-148">La función [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) se usa para ejecutar la consulta SQL en la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-148">The [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used to execute the SQL query against PostgreSQL database.</span></span> <span data-ttu-id="8b2a7-149">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-149">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

<span data-ttu-id="8b2a7-150">Después de que el código se ejecuta correctamente, la salida aparece de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="8b2a7-150">After the code runs successfully, the output appears as follows:</span></span>

![Salida de línea de comandos](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="8b2a7-152">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="8b2a7-152">Read data</span></span>
<span data-ttu-id="8b2a7-153">Use el código siguiente para leer los datos insertados mediante la función [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) con la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-153">Use the following code to read the data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="8b2a7-154">Esta función acepta una consulta y devuelve un conjunto de resultados que se puede iterar mediante el uso de [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="8b2a7-154">This function accepts a query and returns a result set that can be iterated over with the use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="8b2a7-155">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-155">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

## <a name="update-data"></a><span data-ttu-id="8b2a7-156">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="8b2a7-156">Update data</span></span>
<span data-ttu-id="8b2a7-157">Use el código siguiente para actualizar la fila de inventario que insertó anteriormente mediante la función [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) con la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-157">Use the following code to update the inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="8b2a7-158">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-158">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

# Update a data row in the table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="8b2a7-159">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="8b2a7-159">Delete data</span></span>
<span data-ttu-id="8b2a7-160">Use el código siguiente para eliminar un elemento de inventario que insertó anteriormente mediante la función [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) con la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-160">Use the following code to delete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="8b2a7-161">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8b2a7-161">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
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

## <a name="next-steps"></a><span data-ttu-id="8b2a7-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b2a7-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8b2a7-163">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="8b2a7-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
