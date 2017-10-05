---
title: "Conexión a Azure Database for MySQL desde C# | Microsoft Docs"
description: "En este tutorial rápido se proporciona un ejemplo de código de C# (.NET) que puede usar para conectarse a Azure Database for MySQL y consultar datos en este servicio."
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
ms.openlocfilehash: f1488f6b4a240165c71c95f759af73d6b9fd7bfe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="25206-103">Azure Database for MySQL: uso de .NET (C#) para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="25206-103">Azure Database for MySQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="25206-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for MySQL mediante una aplicación de C#.</span><span class="sxs-lookup"><span data-stu-id="25206-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="25206-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="25206-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante C# y que nunca ha utilizado Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="25206-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25206-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="25206-107">Prerequisites</span></span>
<span data-ttu-id="25206-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="25206-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="25206-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="25206-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="25206-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="25206-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="25206-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="25206-111">You also need to:</span></span>
- <span data-ttu-id="25206-112">Instale [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="25206-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="25206-113">Siga los pasos descritos en el artículo vinculado para instalar .NET específicamente para su plataforma (Windows, Ubuntu Linux o macOS).</span><span class="sxs-lookup"><span data-stu-id="25206-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="25206-114">Instale [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="25206-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="25206-115">Instale [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="25206-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="25206-116">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="25206-116">Get connection information</span></span>
<span data-ttu-id="25206-117">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="25206-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="25206-118">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="25206-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="25206-119">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="25206-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="25206-120">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que ha creado, por ejemplo, **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="25206-120">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="25206-121">Haga clic en el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="25206-121">Click the server name.</span></span>
4. <span data-ttu-id="25206-122">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="25206-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="25206-123">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="25206-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="25206-124">![Nombre del servidor de Azure Database for MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="25206-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="25206-125">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="25206-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="25206-126">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="25206-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="25206-127">Use el código siguiente para conectarse y cargar los datos mediante las instrucciones SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="25206-127">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="25206-128">El código usa la clase ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="25206-128">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="25206-129">A continuación, el código usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), establece la propiedad CommandText y llama al método [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-129">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span> 

<span data-ttu-id="25206-130">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-130">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="25206-131">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="25206-131">Read data</span></span>

<span data-ttu-id="25206-132">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="25206-132">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="25206-133">El código usa la clase ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="25206-133">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="25206-134">A continuación, el código usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) y el método [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-134">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) to run the database commands.</span></span> <span data-ttu-id="25206-135">A continuación, el código usa [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) para avanzar a los registros de los resultados.</span><span class="sxs-lookup"><span data-stu-id="25206-135">Next the code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) to advance to the records in the results.</span></span> <span data-ttu-id="25206-136">A continuación, el código usa GetInt32() y GetString() para analizar los valores del registro.</span><span class="sxs-lookup"><span data-stu-id="25206-136">Then the code uses GetInt32 and GetString to parse the values in the record.</span></span>

<span data-ttu-id="25206-137">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-137">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="25206-138">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="25206-138">Update data</span></span>
<span data-ttu-id="25206-139">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="25206-139">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="25206-140">El código usa la clase ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="25206-140">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="25206-141">A continuación, el código usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), establece la propiedad CommandText y llama al método [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-141">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="25206-142">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-142">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="25206-143">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="25206-143">Delete data</span></span>
<span data-ttu-id="25206-144">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="25206-144">Use the following code to connect and delete the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="25206-145">El código usa la clase ODBC con el método [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) para establecer una conexión con MySQL.</span><span class="sxs-lookup"><span data-stu-id="25206-145">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="25206-146">A continuación, el código usa el método [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), establece la propiedad CommandText y llama al método [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-146">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="25206-147">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="25206-147">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="25206-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25206-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="25206-149">Migre su Base de datos MySQL a Azure Database for MySQL mediante el volcado y la restauración</span><span class="sxs-lookup"><span data-stu-id="25206-149">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
