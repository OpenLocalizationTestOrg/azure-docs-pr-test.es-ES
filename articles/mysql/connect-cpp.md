---
title: "Conexión a Azure Database for MySQL desde C++ | Microsoft Docs"
description: "En este tutorial rápido se proporciona un ejemplo de código de C++ que puede usar para conectarse a Azure Database for MySQL y consultar datos en este servicio."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: 63388b83b913d95136140fa4c56af0dbebbdad81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-connectorc-to-connect-and-query-data"></a><span data-ttu-id="b77d9-103">Azure Database for MySQL: uso de Connector/C++ para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="b77d9-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span></span>
<span data-ttu-id="b77d9-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for MySQL mediante una aplicación de C++.</span><span class="sxs-lookup"><span data-stu-id="b77d9-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="b77d9-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b77d9-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b77d9-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante C++ y que nunca ha utilizado Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="b77d9-106">The steps in this article assume that you are familiar with developing using C++, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b77d9-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b77d9-107">Prerequisites</span></span>
<span data-ttu-id="b77d9-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="b77d9-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="b77d9-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="b77d9-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="b77d9-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="b77d9-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="b77d9-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="b77d9-111">You also need to:</span></span>
- <span data-ttu-id="b77d9-112">Instalar [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="b77d9-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="b77d9-113">Instalar [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b77d9-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="b77d9-114">Instalación de [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="b77d9-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="b77d9-115">Instalación de [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="b77d9-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="b77d9-116">Instalación de Visual Studio y .NET</span><span class="sxs-lookup"><span data-stu-id="b77d9-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="b77d9-117">En los pasos de esta sección se supone que está familiarizado con el desarrollo mediante .NET.</span><span class="sxs-lookup"><span data-stu-id="b77d9-117">The steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="b77d9-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b77d9-118">**Windows**</span></span>
1. <span data-ttu-id="b77d9-119">Instale Visual Studio 2017 Community, que es un IDE gratuito, ampliable, rico en contenido y visualmente atractivo para la creación de aplicaciones modernas para Android, iOS, Windows, así como aplicaciones web y de base de datos, y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="b77d9-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="b77d9-120">Puede instalar el paquete completo de .NET Framework o solo .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b77d9-120">You can install either the full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="b77d9-121">Los fragmentos de código del Tutorial de inicio rápido funcionan con cualquiera de las dos opciones.</span><span class="sxs-lookup"><span data-stu-id="b77d9-121">The code snippets in the Quickstart work with either.</span></span> <span data-ttu-id="b77d9-122">Si Visual Studio ya está instalado en el equipo, omita los dos pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="b77d9-122">If you already have Visual Studio installed on your machine, skip the next two steps.</span></span>
   - <span data-ttu-id="b77d9-123">Descargue el [instalador de Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="b77d9-123">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="b77d9-124">Ejecute el instalador y siga las indicaciones para completar la instalación.</span><span class="sxs-lookup"><span data-stu-id="b77d9-124">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="b77d9-125">**Configuración de Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="b77d9-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="b77d9-126">Desde Visual Studio, propiedad del proyecto > propiedades de configuración > C/C++ > vinculador > general > directorios de bibliotecas adicionales, agregue el directorio lib\opt (es decir, C:\Archivos de programa (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) del conector c++.</span><span class="sxs-lookup"><span data-stu-id="b77d9-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add the lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the c++ connector.</span></span>
2. <span data-ttu-id="b77d9-127">Desde Visual Studio, propiedad de proyecto > propiedades de configuración > C/C++ > general > directorios de inclusión adicionales</span><span class="sxs-lookup"><span data-stu-id="b77d9-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="b77d9-128">Agregue el directorio include/ del conector de c ++ (es decir, C:\Archivos de programa (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="b77d9-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="b77d9-129">Agregue el directorio raíz de la biblioteca Boost (es decir, C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="b77d9-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="b77d9-130">Desde Visual Studio, propiedad de proyecto > propiedades de configuración > C/C++ > vinculador > Entrada > Dependencias adicionales, agregue mysqlcppconn.lib en el campo de texto</span><span class="sxs-lookup"><span data-stu-id="b77d9-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into the text field</span></span>
4. <span data-ttu-id="b77d9-131">Copie el archivo mysqlcppconn.dll desde la carpeta de biblioteca c++ connector en el paso 3 al mismo directorio que la aplicación ejecutable o agréguelo a la variable de entorno para que la aplicación pueda encontrarlo.</span><span class="sxs-lookup"><span data-stu-id="b77d9-131">Either copy mysqlcppconn.dll from the c++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b77d9-132">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="b77d9-132">Get connection information</span></span>
<span data-ttu-id="b77d9-133">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="b77d9-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="b77d9-134">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b77d9-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b77d9-135">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b77d9-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b77d9-136">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que ha creado, por ejemplo, **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="b77d9-136">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="b77d9-137">Haga clic en el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="b77d9-137">Click the server name.</span></span>
4. <span data-ttu-id="b77d9-138">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="b77d9-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="b77d9-139">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="b77d9-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b77d9-140">![Nombre del servidor de Azure Database for MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b77d9-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b77d9-141">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="b77d9-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b77d9-142">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="b77d9-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="b77d9-143">Use el código siguiente para conectarse y cargar los datos mediante las instrucciones SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="b77d9-143">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="b77d9-144">El código usa la clase sql::Driver con el método connect() para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="b77d9-144">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b77d9-145">A continuación, el código usa los métodos createStatement() y execute() para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="b77d9-145">Then the code uses method createStatement() and execute() to run the database commands.</span></span> 

<span data-ttu-id="b77d9-146">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b77d9-146">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="b77d9-147">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="b77d9-147">Read data</span></span>

<span data-ttu-id="b77d9-148">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="b77d9-148">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="b77d9-149">El código usa la clase sql::Driver con el método connect() para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="b77d9-149">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b77d9-150">A continuación, el código usa los métodos prepareStatement() y executeQuery() para ejecutar los comandos de selección.</span><span class="sxs-lookup"><span data-stu-id="b77d9-150">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span></span> <span data-ttu-id="b77d9-151">Finalmente, el código usa next() para avanzar a los registros de los resultados.</span><span class="sxs-lookup"><span data-stu-id="b77d9-151">Finally the code uses next() to advance to the records in the results.</span></span> <span data-ttu-id="b77d9-152">A continuación, el código usa getInt() and getString() para analizar los valores del registro.</span><span class="sxs-lookup"><span data-stu-id="b77d9-152">Then the code uses getInt() and getString() to parse the values in the record.</span></span>

<span data-ttu-id="b77d9-153">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b77d9-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="b77d9-154">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="b77d9-154">Update data</span></span>
<span data-ttu-id="b77d9-155">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="b77d9-155">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="b77d9-156">El código usa la clase sql::Driver con el método connect() para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="b77d9-156">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b77d9-157">A continuación, el código usa los métodos prepareStatement() y executeQuery() para ejecutar los comandos de actualización.</span><span class="sxs-lookup"><span data-stu-id="b77d9-157">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span></span> 

<span data-ttu-id="b77d9-158">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b77d9-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="b77d9-159">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="b77d9-159">Delete data</span></span>
<span data-ttu-id="b77d9-160">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="b77d9-160">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="b77d9-161">El código usa la clase sql::Driver con el método connect() para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="b77d9-161">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b77d9-162">A continuación, el código usa los métodos prepareStatement() y executeQuery() para ejecutar los comandos de eliminación.</span><span class="sxs-lookup"><span data-stu-id="b77d9-162">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span></span>

<span data-ttu-id="b77d9-163">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b77d9-163">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="b77d9-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b77d9-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b77d9-165">Migre su Base de datos MySQL a Azure Database for MySQL mediante el volcado y la restauración</span><span class="sxs-lookup"><span data-stu-id="b77d9-165">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
