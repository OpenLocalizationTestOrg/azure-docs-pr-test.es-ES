---
title: "Conexión a Azure Database for MySQL desde Python | Microsoft Docs"
description: "En este tutorial rápido se proporcionan varios ejemplos de código de Python que se pueden usar para conectarse a Azure Database for MySQL y consultar datos en este servicio."
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
ms.openlocfilehash: 4c3a2e65b83fab6fe5b8b7778782a747bb5e9cf9
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-python-to-connect-and-query-data"></a><span data-ttu-id="609f5-103">Azure Database for MySQL: uso de Python para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="609f5-103">Azure Database for MySQL: Use Python to connect and query data</span></span>
<span data-ttu-id="609f5-104">En este tutorial rápido se muestra cómo usar [Python](https://python.org) para conectarse a una instancia de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="609f5-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for MySQL.</span></span> <span data-ttu-id="609f5-105">Se emplean instrucciones SQL para consultar, insertar, actualizar y eliminar datos de la base de datos en las plataformas Mac OS, Ubuntu Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="609f5-105">It uses SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="609f5-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante Python, pero que nunca ha trabajado con Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="609f5-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="609f5-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="609f5-107">Prerequisites</span></span>
<span data-ttu-id="609f5-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="609f5-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="609f5-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="609f5-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="609f5-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="609f5-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-python-and-the-mysql-connector"></a><span data-ttu-id="609f5-111">Instalación de Python y el conector de MySQL</span><span class="sxs-lookup"><span data-stu-id="609f5-111">Install Python and the MySQL connector</span></span>
<span data-ttu-id="609f5-112">Instale [Python](https://www.python.org/downloads/) y el [conector de MySQL para Python](https://dev.mysql.com/downloads/connector/python/) en su propia máquina.</span><span class="sxs-lookup"><span data-stu-id="609f5-112">Install [Python](https://www.python.org/downloads/) and the [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="609f5-113">Dependiendo de la plataforma, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="609f5-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="609f5-114">Windows</span><span class="sxs-lookup"><span data-stu-id="609f5-114">Windows</span></span>
1. <span data-ttu-id="609f5-115">Descargue e instale Python 2.7 desde [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="609f5-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="609f5-116">Para comprobar la instalación de Python, inicie el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="609f5-116">Check the Python installation by launching the command prompt.</span></span> <span data-ttu-id="609f5-117">Ejecute el comando `C:\python27\python.exe -V` mediante el modificador V mayúscula para ver el número de versión.</span><span class="sxs-lookup"><span data-stu-id="609f5-117">Run the command `C:\python27\python.exe -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="609f5-118">Instale el conector de Python para MySQL desde [mysql.com](https://dev.mysql.com/downloads/connector/python/) que corresponda a su versión de Python.</span><span class="sxs-lookup"><span data-stu-id="609f5-118">Install the Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding to your version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="609f5-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="609f5-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="609f5-120">En Linux (Ubuntu), Python se instala normalmente como parte de la instalación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="609f5-120">In Linux (Ubuntu), Python is typically installed as part of the default installation.</span></span>
2. <span data-ttu-id="609f5-121">Para comprobar la instalación de Python, inicie el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="609f5-121">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="609f5-122">Ejecute el comando `python -V` mediante el modificador V mayúscula para ver el número de versión.</span><span class="sxs-lookup"><span data-stu-id="609f5-122">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="609f5-123">Para comprobar la instalación de PIP, ejecute el comando `pip show pip -V` para ver el número de versión.</span><span class="sxs-lookup"><span data-stu-id="609f5-123">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span> 
4. <span data-ttu-id="609f5-124">PIP puede estar incluido en algunas versiones de Python.</span><span class="sxs-lookup"><span data-stu-id="609f5-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="609f5-125">Si PIP no está instalado, puede instalar el paquete [PIP] (https://pip.pypa.io/en/stable/installing/) mediante la ejecución de comando `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="609f5-125">If PIP is not installed, you may install the [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="609f5-126">Actualice PIP a la versión más reciente mediante la ejecución del comando `pip install -U pip`.</span><span class="sxs-lookup"><span data-stu-id="609f5-126">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="609f5-127">Instale el conector de MySQL para Python y sus dependencias mediante el comando PIP:</span><span class="sxs-lookup"><span data-stu-id="609f5-127">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="609f5-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="609f5-128">MacOS</span></span>
1. <span data-ttu-id="609f5-129">En Mac OS, Python se instala normalmente como parte de la instalación predeterminada del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="609f5-129">In Mac OS, Python is typically installed as part of the default OS installation.</span></span>
2. <span data-ttu-id="609f5-130">Para comprobar la instalación de Python, inicie el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="609f5-130">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="609f5-131">Ejecute el comando `python -V` mediante el modificador V mayúscula para ver el número de versión.</span><span class="sxs-lookup"><span data-stu-id="609f5-131">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="609f5-132">Para comprobar la instalación de PIP, ejecute el comando `pip show pip -V` para ver el número de versión.</span><span class="sxs-lookup"><span data-stu-id="609f5-132">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span>
4. <span data-ttu-id="609f5-133">PIP puede estar incluido en algunas versiones de Python.</span><span class="sxs-lookup"><span data-stu-id="609f5-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="609f5-134">Si PIP no está instalado, puede instalar el paquete de [PIP](https://pip.pypa.io/en/stable/installing/).</span><span class="sxs-lookup"><span data-stu-id="609f5-134">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="609f5-135">Actualice PIP a la versión más reciente mediante la ejecución del comando `pip install -U pip`.</span><span class="sxs-lookup"><span data-stu-id="609f5-135">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="609f5-136">Instale el conector de MySQL para Python y sus dependencias mediante el comando PIP:</span><span class="sxs-lookup"><span data-stu-id="609f5-136">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="609f5-137">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="609f5-137">Get connection information</span></span>
<span data-ttu-id="609f5-138">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="609f5-138">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="609f5-139">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="609f5-139">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="609f5-140">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="609f5-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="609f5-141">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que ha creado, por ejemplo, **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="609f5-141">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="609f5-142">Haga clic en el nombre del servidor **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="609f5-142">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="609f5-143">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="609f5-143">Select the server's **Properties** page.</span></span> <span data-ttu-id="609f5-144">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="609f5-144">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="609f5-145">![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="609f5-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="609f5-146">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="609f5-146">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="609f5-147">Ejecución de código de Python</span><span class="sxs-lookup"><span data-stu-id="609f5-147">Run Python Code</span></span>
- <span data-ttu-id="609f5-148">Pegue el código en un archivo de texto y guarde el archivo en una carpeta de proyecto con la extensión de archivo .py, por ejemplo, C:\pythonmysql\createtable.py o /home/username/pythonmysql/createtable.py</span><span class="sxs-lookup"><span data-stu-id="609f5-148">Paste the code into a text file, and save the file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="609f5-149">Para ejecutar el código, inicie el símbolo del sistema o el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="609f5-149">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="609f5-150">Cambie el directorio a la carpeta de proyecto `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="609f5-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="609f5-151">A continuación, escriba el comando python seguido del nombre de archivo `python createtable.py` para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="609f5-151">Then type the python command followed by the file name `python createtable.py` to run the application.</span></span> <span data-ttu-id="609f5-152">En el sistema operativo Windows, si no se encuentra python.exe, puede proporcionar la ruta de acceso completa al archivo ejecutable o agregar la ruta de acceso de Python en la variable de entorno path.</span><span class="sxs-lookup"><span data-stu-id="609f5-152">On the Windows OS, if python.exe is not found, you may provide the full path to the executable, or add the Python path into the path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="609f5-153">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="609f5-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="609f5-154">Use el código siguiente para conectarse al servidor, crear una tabla y cargar los datos mediante una instrucción SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="609f5-154">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="609f5-155">En el código, se importa la biblioteca mysql.connector.</span><span class="sxs-lookup"><span data-stu-id="609f5-155">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="609f5-156">La función [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) se usa para conectarse a Azure Database for MySQL mediante los [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) de la colección config.</span><span class="sxs-lookup"><span data-stu-id="609f5-156">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="609f5-157">El código usa un cursor en la conexión, y el método [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) ejecuta la consulta SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="609f5-157">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="609f5-158">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="609f5-158">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
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

## <a name="read-data"></a><span data-ttu-id="609f5-159">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="609f5-159">Read data</span></span>
<span data-ttu-id="609f5-160">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="609f5-160">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="609f5-161">En el código, se importa la biblioteca mysql.connector.</span><span class="sxs-lookup"><span data-stu-id="609f5-161">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="609f5-162">La función [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) se usa para conectarse a Azure Database for MySQL mediante los [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) de la colección config.</span><span class="sxs-lookup"><span data-stu-id="609f5-162">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="609f5-163">El código usa un cursor en la conexión, y el método [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) ejecuta la instrucción SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="609f5-163">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> <span data-ttu-id="609f5-164">Las filas de datos se leen mediante el método [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html).</span><span class="sxs-lookup"><span data-stu-id="609f5-164">The data rows are read using the [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="609f5-165">El conjunto de resultados se mantiene en una fila de la colección y se usa un iterador for para recorrer en iteración las filas.</span><span class="sxs-lookup"><span data-stu-id="609f5-165">The result set is kept in a collection row and a for iterator is used to loop over the rows.</span></span>

<span data-ttu-id="609f5-166">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="609f5-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
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

## <a name="update-data"></a><span data-ttu-id="609f5-167">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="609f5-167">Update data</span></span>
<span data-ttu-id="609f5-168">Use el código siguiente para conectarse y actualizar los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="609f5-168">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="609f5-169">En el código, se importa la biblioteca mysql.connector.</span><span class="sxs-lookup"><span data-stu-id="609f5-169">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="609f5-170">La función [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) se usa para conectarse a Azure Database for MySQL mediante los [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) de la colección config.</span><span class="sxs-lookup"><span data-stu-id="609f5-170">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="609f5-171">El código usa un cursor en la conexión, y el método [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) ejecuta la instrucción SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="609f5-171">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> 

<span data-ttu-id="609f5-172">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="609f5-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in the table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="609f5-173">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="609f5-173">Delete data</span></span>
<span data-ttu-id="609f5-174">Use el código siguiente para conectarse y eliminar datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="609f5-174">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="609f5-175">En el código, se importa la biblioteca mysql.connector.</span><span class="sxs-lookup"><span data-stu-id="609f5-175">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="609f5-176">La función [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) se usa para conectarse a Azure Database for MySQL mediante los [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) de la colección config.</span><span class="sxs-lookup"><span data-stu-id="609f5-176">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="609f5-177">El código usa un cursor en la conexión, y el método [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) ejecuta la consulta SQL en la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="609f5-177">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="609f5-178">Reemplace los parámetros `host`, `user`, `password` y `database` por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="609f5-178">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in the table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="609f5-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="609f5-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="609f5-180">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="609f5-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
