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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="444d6-103">Base de datos de Azure para MySQL: uso de Python tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="444d6-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="444d6-104">Este tutorial rápido muestra cómo toouse [Python](https://python.org) tooconnect tooan base de datos de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="444d6-105">Usa tooquery de instrucciones SQL, insert, update y delete datos en base de datos de hello en plataformas Windows, Mac OS y Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="444d6-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="444d6-106">pasos de Hello en este artículo se supone que está familiarizado con el desarrollo con Python y son tooworking nueva con la base de datos de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="444d6-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="444d6-107">Prerequisites</span></span>
<span data-ttu-id="444d6-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="444d6-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="444d6-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="444d6-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="444d6-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="444d6-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="444d6-111">Instalar Python y Hola conector MySQL</span><span class="sxs-lookup"><span data-stu-id="444d6-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="444d6-112">Instalar [Python](https://www.python.org/downloads/) hello y [conector MySQL de Python](https://dev.mysql.com/downloads/connector/python/) en su propio equipo.</span><span class="sxs-lookup"><span data-stu-id="444d6-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="444d6-113">Dependiendo de la plataforma, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="444d6-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="444d6-114">Windows</span><span class="sxs-lookup"><span data-stu-id="444d6-114">Windows</span></span>
1. <span data-ttu-id="444d6-115">Descargue e instale Python 2.7 desde [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="444d6-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="444d6-116">Comprobar instalación de Python Hola iniciando Hola símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="444d6-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="444d6-117">Ejecute el comando de hello `C:\python27\python.exe -V` con número de versión de Hola mayúsculas V conmutador toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="444d6-118">Instalar el conector de Python de Hola para MySQL desde [mysql.com](https://dev.mysql.com/downloads/connector/python/) versión tooyour correspondiente de Python.</span><span class="sxs-lookup"><span data-stu-id="444d6-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="444d6-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="444d6-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="444d6-120">Linux (Ubuntu), Python normalmente se instala como parte de la instalación predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="444d6-121">Compruebe la instalación de Python de hello iniciando el shell de bash Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="444d6-122">Ejecute el comando de hello `python -V` con número de versión de Hola mayúsculas V conmutador toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="444d6-123">Comprobar instalación de PIP de hello ejecutando hello `pip show pip -V` número de versión de hello toosee de comandos.</span><span class="sxs-lookup"><span data-stu-id="444d6-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="444d6-124">PIP puede estar incluido en algunas versiones de Python.</span><span class="sxs-lookup"><span data-stu-id="444d6-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="444d6-125">Si no está instalado el PIP, puede instalar Hola [PIP] (https://pip.pypa.io/en/stable/installing/) paquete, mediante la ejecución de comando `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="444d6-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="444d6-126">Actualización PIP toohello versión más reciente, mediante la ejecución de hello `pip install -U pip` comando.</span><span class="sxs-lookup"><span data-stu-id="444d6-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="444d6-127">Instale el conector de MySQL de Hola para Python y sus dependencias mediante Hola PIP comando:</span><span class="sxs-lookup"><span data-stu-id="444d6-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="444d6-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="444d6-128">MacOS</span></span>
1. <span data-ttu-id="444d6-129">En Mac OS, Python normalmente se instala como parte de la instalación del SO predeterminado Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="444d6-130">Compruebe la instalación de Python de hello iniciando el shell de bash Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="444d6-131">Ejecute el comando de hello `python -V` con número de versión de Hola mayúsculas V conmutador toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="444d6-132">Comprobar instalación de PIP de hello ejecutando hello `pip show pip -V` número de versión de hello toosee de comandos.</span><span class="sxs-lookup"><span data-stu-id="444d6-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="444d6-133">PIP puede estar incluido en algunas versiones de Python.</span><span class="sxs-lookup"><span data-stu-id="444d6-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="444d6-134">Si no está instalado el PIP, puede instalar hello [PIP](https://pip.pypa.io/en/stable/installing/) paquete.</span><span class="sxs-lookup"><span data-stu-id="444d6-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="444d6-135">Actualización PIP toohello versión más reciente, mediante la ejecución de hello `pip install -U pip` comando.</span><span class="sxs-lookup"><span data-stu-id="444d6-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="444d6-136">Instale el conector de MySQL de Hola para Python y sus dependencias mediante Hola PIP comando:</span><span class="sxs-lookup"><span data-stu-id="444d6-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="444d6-137">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="444d6-137">Get connection information</span></span>
<span data-ttu-id="444d6-138">Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="444d6-139">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="444d6-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="444d6-140">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="444d6-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="444d6-141">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque servidor hello plegado, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="444d6-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="444d6-142">Haga clic en el nombre del servidor de hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="444d6-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="444d6-143">Servidor de hello seleccione **propiedades** página.</span><span class="sxs-lookup"><span data-stu-id="444d6-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="444d6-144">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="444d6-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="444d6-145">![Azure Database for MySQL: inicio de sesión del Administrador del servidor](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="444d6-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="444d6-146">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="444d6-147">Ejecución de código de Python</span><span class="sxs-lookup"><span data-stu-id="444d6-147">Run Python Code</span></span>
- <span data-ttu-id="444d6-148">Pegue el código de hello en un archivo de texto y guarde el archivo hello en una carpeta del proyecto con .py de extensión de archivo, como C:\pythonmysql\createtable.py o /home/username/pythonmysql/createtable.py</span><span class="sxs-lookup"><span data-stu-id="444d6-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="444d6-149">código de hello toorun, inicie el símbolo del sistema de Hola o el shell de bash.</span><span class="sxs-lookup"><span data-stu-id="444d6-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="444d6-150">Cambie el directorio a la carpeta de proyecto `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="444d6-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="444d6-151">A continuación, escriba el comando de python de hello seguido por el nombre de archivo de hello `python createtable.py` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="444d6-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="444d6-152">En el sistema operativo Windows hello, si no se encuentra python.exe, puede proporcionar toohello de ruta de acceso completa de hello ejecutable o agregar la ruta de acceso de Python de hello en la variable de entorno path de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="444d6-153">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="444d6-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="444d6-154">Siguiente Hola de uso codificar tooconnect toohello server, cree una tabla y cargar datos de hello mediante un **insertar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="444d6-155">En el código de hello, se importa la biblioteca de mysql.connector Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="444d6-156">Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="444d6-157">código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la consulta SQL de hello en base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="444d6-158">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="444d6-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="444d6-159">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="444d6-159">Read data</span></span>
<span data-ttu-id="444d6-160">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="444d6-161">En el código de hello, se importa la biblioteca de mysql.connector Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="444d6-162">Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="444d6-163">código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la instrucción de SQL de hello en base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="444d6-164">las filas de datos de Hola se leen con hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) método.</span><span class="sxs-lookup"><span data-stu-id="444d6-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="444d6-165">conjunto de resultados Hello se mantiene una en una fila de la colección y una para iterador es tooloop utilizado en filas de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="444d6-166">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="444d6-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="444d6-167">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="444d6-167">Update data</span></span>
<span data-ttu-id="444d6-168">Código tooconnect siguiente de Hola de uso y actualizar Hola datos mediante un **actualizar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="444d6-169">En el código de hello, se importa la biblioteca de mysql.connector Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="444d6-170">Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="444d6-171">código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la instrucción de SQL de hello en base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="444d6-172">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="444d6-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="444d6-173">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="444d6-173">Delete data</span></span>
<span data-ttu-id="444d6-174">Código tooconnect siguiente de Hola de uso y eliminar los datos mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="444d6-175">En el código de hello, se importa la biblioteca de mysql.connector Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="444d6-176">Hola [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) función es tooconnect usado tooAzure base de datos de MySQL con hello [argumentos de conexión](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) en la colección de configuraciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="444d6-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="444d6-177">código de Hello usa un cursor sobre la conexión de hello, y [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) método ejecuta la consulta SQL de hello en base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="444d6-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="444d6-178">Reemplace hello `host`, `user`, `password`, y `database` parámetros con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="444d6-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="444d6-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="444d6-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="444d6-180">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="444d6-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
