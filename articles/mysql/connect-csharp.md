---
title: Conectar tooAzure base de datos de MySQL desde C# | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo código de C# (. NET) puede usar tooconnect y consultar los datos de la base de datos MySQL."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="0e38b-103">Base de datos de Azure para MySQL: Use .NET (C#) tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="0e38b-103">Azure Database for MySQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="0e38b-104">Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos de MySQL mediante una aplicación de C#.</span><span class="sxs-lookup"><span data-stu-id="0e38b-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="0e38b-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="0e38b-106">Hello pasos en este artículo se supone que está familiarizado con el desarrollo con C#, y que tooworking nueva con la base de datos de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="0e38b-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e38b-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e38b-107">Prerequisites</span></span>
<span data-ttu-id="0e38b-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="0e38b-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="0e38b-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="0e38b-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="0e38b-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="0e38b-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="0e38b-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="0e38b-111">You also need to:</span></span>
- <span data-ttu-id="0e38b-112">Instale [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="0e38b-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="0e38b-113">Siga los pasos de Hola Hola vinculado artículo tooinstall .NET específicamente para la plataforma (Windows, Ubuntu Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="0e38b-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="0e38b-114">Instale [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0e38b-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="0e38b-115">Instale [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="0e38b-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0e38b-116">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="0e38b-116">Get connection information</span></span>
<span data-ttu-id="0e38b-117">Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="0e38b-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="0e38b-118">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="0e38b-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0e38b-119">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0e38b-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0e38b-120">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="0e38b-120">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="0e38b-121">Haga clic en el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-121">Click hello server name.</span></span>
4. <span data-ttu-id="0e38b-122">Servidor de hello seleccione **propiedades** página.</span><span class="sxs-lookup"><span data-stu-id="0e38b-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="0e38b-123">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="0e38b-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0e38b-124">![Nombre del servidor de Azure Database for MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="0e38b-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="0e38b-125">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="0e38b-126">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="0e38b-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="0e38b-127">Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL.</span><span class="sxs-lookup"><span data-stu-id="0e38b-127">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="0e38b-128">código de Hello usa la clase de ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="0e38b-128">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="0e38b-129">A continuación, el código de hello usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-129">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span> 

<span data-ttu-id="0e38b-130">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0e38b-130">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="0e38b-131">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="0e38b-131">Read data</span></span>

<span data-ttu-id="0e38b-132">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="0e38b-132">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="0e38b-133">código de Hello usa la clase de ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="0e38b-133">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="0e38b-134">A continuación, el código de hello usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) y método [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-134">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello database commands.</span></span> <span data-ttu-id="0e38b-135">A continuación Hola código usa [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello registros en los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-135">Next hello code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="0e38b-136">A continuación, código de hello usa GetInt32 y GetString valores de hello de tooparse en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="0e38b-136">Then hello code uses GetInt32 and GetString tooparse hello values in hello record.</span></span>

<span data-ttu-id="0e38b-137">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0e38b-137">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="0e38b-138">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="0e38b-138">Update data</span></span>
<span data-ttu-id="0e38b-139">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="0e38b-139">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="0e38b-140">código de Hello usa la clase de ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="0e38b-140">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="0e38b-141">A continuación, el código de hello usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-141">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="0e38b-142">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0e38b-142">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="0e38b-143">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="0e38b-143">Delete data</span></span>
<span data-ttu-id="0e38b-144">Código tooconnect siguiente de Hola de uso y eliminar datos de hello con un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="0e38b-144">Use hello following code tooconnect and delete hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="0e38b-145">código de Hello usa la clase de ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish una tooMySQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="0e38b-145">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="0e38b-146">A continuación, el código de hello usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="0e38b-146">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="0e38b-147">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0e38b-147">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="0e38b-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e38b-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0e38b-149">Migrar su tooAzure de base de datos base de datos de MySQL para uso de volcado de memoria y la restauración de MySQL</span><span class="sxs-lookup"><span data-stu-id="0e38b-149">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
