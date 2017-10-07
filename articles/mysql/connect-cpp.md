---
title: Conectar tooAzure base de datos de MySQL desde C++ | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo de código de C++ puede utilizar tooconnect y consultar los datos de la base de datos MySQL."
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
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="77706-103">Base de datos de Azure para MySQL: Use conector c/c ++ tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="77706-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="77706-104">Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos de MySQL mediante una aplicación de C++.</span><span class="sxs-lookup"><span data-stu-id="77706-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="77706-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="77706-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="77706-106">Hello pasos descritos en este artículo se suponen que está familiarizado con el desarrollo con C++ y que son tooworking nueva con la base de datos de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="77706-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77706-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="77706-107">Prerequisites</span></span>
<span data-ttu-id="77706-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="77706-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="77706-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="77706-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="77706-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="77706-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="77706-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="77706-111">You also need to:</span></span>
- <span data-ttu-id="77706-112">Instalar [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="77706-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="77706-113">Instalar [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="77706-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="77706-114">Instalación de [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="77706-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="77706-115">Instalación de [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="77706-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="77706-116">Instalación de Visual Studio y .NET</span><span class="sxs-lookup"><span data-stu-id="77706-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="77706-117">pasos de Hello en esta sección se supone que está familiarizado con el desarrollo con. NET.</span><span class="sxs-lookup"><span data-stu-id="77706-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="77706-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="77706-118">**Windows**</span></span>
1. <span data-ttu-id="77706-119">Instale Visual Studio 2017 Community, que es un IDE gratuito, ampliable, rico en contenido y visualmente atractivo para la creación de aplicaciones modernas para Android, iOS, Windows, así como aplicaciones web y de base de datos, y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="77706-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="77706-120">Puede instalar Hola completa de .NET Framework o simplemente .NET Core.</span><span class="sxs-lookup"><span data-stu-id="77706-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="77706-121">fragmentos de código de Hello en hello inicio rápido de trabajar con cualquiera.</span><span class="sxs-lookup"><span data-stu-id="77706-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="77706-122">Si ya tiene Visual Studio instalados en su equipo, omita Hola dos pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="77706-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="77706-123">Descargar hello [instalador de Visual Studio de 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="77706-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="77706-124">Ejecute el programa de instalación de Hola y siga Hola instalación indicaciones toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="77706-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="77706-125">**Configuración de Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="77706-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="77706-126">Desde Visual Studio, la propiedad de proyecto > Propiedades de configuración > C/C++ > vinculador > general > directorios de bibliotecas adicionales, agregue el directorio de lib\opt de hello (es decir,: C:\Program Files (x86) \MySQL\MySQL conector C++ 1.1.9\lib\opt) de hello c ++ conector.</span><span class="sxs-lookup"><span data-stu-id="77706-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="77706-127">Desde Visual Studio, propiedad de proyecto > propiedades de configuración > C/C++ > general > directorios de inclusión adicionales</span><span class="sxs-lookup"><span data-stu-id="77706-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="77706-128">Agregue el directorio include/ del conector de c ++ (es decir, C:\Archivos de programa (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="77706-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="77706-129">Agregue el directorio raíz de la biblioteca Boost (es decir, C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="77706-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="77706-130">Desde Visual Studio, la propiedad de proyecto > Propiedades de configuración > C/C++ > vinculador > entrada > dependencias adicionales, agregue mysqlcppconn.lib en el campo de texto hello</span><span class="sxs-lookup"><span data-stu-id="77706-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="77706-131">Cualquier mysqlcppconn.dll de copia de hello c ++ conector carpeta library en paso 3 toohello mismo directorio que el ejecutable de la aplicación hello o Agregar variable de entorno toohello para que la aplicación pueda encontrarlo.</span><span class="sxs-lookup"><span data-stu-id="77706-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="77706-132">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="77706-132">Get connection information</span></span>
<span data-ttu-id="77706-133">Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="77706-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="77706-134">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="77706-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="77706-135">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77706-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="77706-136">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="77706-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="77706-137">Haga clic en el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="77706-137">Click hello server name.</span></span>
4. <span data-ttu-id="77706-138">Servidor de hello seleccione **propiedades** página.</span><span class="sxs-lookup"><span data-stu-id="77706-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="77706-139">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="77706-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="77706-140">![Nombre del servidor de Azure Database for MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="77706-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="77706-141">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="77706-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="77706-142">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="77706-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="77706-143">Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL.</span><span class="sxs-lookup"><span data-stu-id="77706-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="77706-144">código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="77706-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="77706-145">A continuación, código de hello usa método createStatement() y Execute toorun Hola comandos base de datos.</span><span class="sxs-lookup"><span data-stu-id="77706-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="77706-146">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="77706-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="read-data"></a><span data-ttu-id="77706-147">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="77706-147">Read data</span></span>

<span data-ttu-id="77706-148">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="77706-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="77706-149">código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="77706-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="77706-150">A continuación, código de hello usa el método prepareStatement() y executeQuery() toorun Hola seleccionar comandos.</span><span class="sxs-lookup"><span data-stu-id="77706-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="77706-151">Por último código de hello usa next() tooadvance toohello registros en los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="77706-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="77706-152">A continuación, el código de hello usa valores de hello tooparse getInt() y getString() en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="77706-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="77706-153">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="77706-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="update-data"></a><span data-ttu-id="77706-154">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="77706-154">Update data</span></span>
<span data-ttu-id="77706-155">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="77706-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="77706-156">código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="77706-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="77706-157">A continuación, código de hello usa método prepareStatement() y executeQuery() toorun Hola comandos de actualización.</span><span class="sxs-lookup"><span data-stu-id="77706-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="77706-158">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="77706-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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


## <a name="delete-data"></a><span data-ttu-id="77706-159">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="77706-159">Delete data</span></span>
<span data-ttu-id="77706-160">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="77706-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="77706-161">código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="77706-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="77706-162">A continuación, código de hello usa método prepareStatement() y executeQuery() toorun Hola eliminar comandos.</span><span class="sxs-lookup"><span data-stu-id="77706-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="77706-163">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="77706-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="next-steps"></a><span data-ttu-id="77706-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77706-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="77706-165">Migrar su tooAzure de base de datos base de datos de MySQL para uso de volcado de memoria y la restauración de MySQL</span><span class="sxs-lookup"><span data-stu-id="77706-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
