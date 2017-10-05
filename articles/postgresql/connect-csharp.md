---
title: "Conexión a Azure Database for PostgreSQL desde C# | Microsoft Docs"
description: "En este tutorial rápido se proporciona un ejemplo de código de C# (.NET) que puede usar para conectarse a Azure Database for PostgreSQL y consultar datos en este servicio."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 91e0269e310688dc88d139430ccf386a1d26a61c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="c4db9-103">Azure Database for PostgreSQL: uso de .NET (C#) para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="c4db9-103">Azure Database for PostgreSQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="c4db9-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for PostgreSQL mediante una aplicación de C#.</span><span class="sxs-lookup"><span data-stu-id="c4db9-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="c4db9-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="c4db9-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante C#, pero que nunca ha trabajado con Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4db9-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4db9-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c4db9-107">Prerequisites</span></span>
<span data-ttu-id="c4db9-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="c4db9-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c4db9-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c4db9-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="c4db9-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="c4db9-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="c4db9-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="c4db9-111">You also need to:</span></span>
- <span data-ttu-id="c4db9-112">Instale [.NET Framework](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="c4db9-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="c4db9-113">Siga los pasos descritos en el artículo vinculado para instalar .NET específicamente para su plataforma (Windows, Ubuntu Linux o macOS).</span><span class="sxs-lookup"><span data-stu-id="c4db9-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="c4db9-114">Instale [Visual Studio](https://www.visualstudio.com/downloads/) o Visual Studio Code para escribir y editar el código.</span><span class="sxs-lookup"><span data-stu-id="c4db9-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code to type and edit code.</span></span>
- <span data-ttu-id="c4db9-115">Instale la biblioteca [Npgsql](http://www.npgsql.org/doc/index.html), tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="c4db9-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="c4db9-116">Instalación de referencias de Npgsql en la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4db9-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="c4db9-117">Para conectarse a PostgreSQL desde las aplicaciones de C#, use la biblioteca ADO.NET de código abierto llamada Npgsql.</span><span class="sxs-lookup"><span data-stu-id="c4db9-117">To connect from the C# application to PostgreSQL, use the open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="c4db9-118">NuGet ayuda a descargar y administrar fácilmente las referencias.</span><span class="sxs-lookup"><span data-stu-id="c4db9-118">NuGet helps download and manage the references easily.</span></span>

1. <span data-ttu-id="c4db9-119">Cree una nueva solución de C# o abra una existente:</span><span class="sxs-lookup"><span data-stu-id="c4db9-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="c4db9-120">En Visual Studio, cree una solución; para ello, haga clic en el menú Archivo **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="c4db9-121">En el cuadro de diálogo Nuevo proyecto, expanda **Plantillas** > **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-121">In the New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="c4db9-122">Elija una plantilla adecuada, por ejemplo, **Aplicación de consola (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="c4db9-123">Use el Administrador de paquetes Nuget para instalar Npgsql:</span><span class="sxs-lookup"><span data-stu-id="c4db9-123">Use the Nuget Package Manager to install Npgsql:</span></span>
   - <span data-ttu-id="c4db9-124">Haga clic en el menú **Herramientas** > **Administrador de paquetes NuGet** > **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-124">Click the **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="c4db9-125">En la **Consola del Administrador de paquetes**, escriba `Install-Package Npgsql`.</span><span class="sxs-lookup"><span data-stu-id="c4db9-125">In the **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="c4db9-126">El comando de instalación descarga el archivo Npgsql.dll y los ensamblados relacionados y los agrega como dependencias en la solución.</span><span class="sxs-lookup"><span data-stu-id="c4db9-126">The install command downloads the Npgsql.dll and related assemblies and adds them as dependencies in the solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c4db9-127">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="c4db9-127">Get connection information</span></span>
<span data-ttu-id="c4db9-128">Obtenga la información de conexión necesaria para conectarse a Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4db9-128">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c4db9-129">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c4db9-129">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c4db9-130">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c4db9-130">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c4db9-131">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que ha creado, por ejemplo, **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-131">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="c4db9-132">Haga clic en el nombre del servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-132">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="c4db9-133">Seleccione la página **Introducción** del servidor.</span><span class="sxs-lookup"><span data-stu-id="c4db9-133">Select the server's **Overview** page.</span></span> <span data-ttu-id="c4db9-134">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="c4db9-134">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c4db9-135">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="c4db9-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="c4db9-136">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c4db9-136">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="c4db9-137">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="c4db9-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="c4db9-138">Use el código siguiente para conectarse y cargar los datos mediante las instrucciones SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-138">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="c4db9-139">El código usa la clase NpgsqlCommand con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) para establecer una conexión a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4db9-139">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="c4db9-140">A continuación, el código usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), establece la propiedad CommandText y llama al método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-140">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span> 

<span data-ttu-id="c4db9-141">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-141">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
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

## <a name="read-data"></a><span data-ttu-id="c4db9-142">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="c4db9-142">Read data</span></span>
<span data-ttu-id="c4db9-143">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-143">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="c4db9-144">El código usa la clase NpgsqlCommand con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) para establecer una conexión a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4db9-144">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="c4db9-145">A continuación, el código usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) y el método [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-145">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) to run the database commands.</span></span> <span data-ttu-id="c4db9-146">A continuación, el código usa [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) para avanzar a los registros de los resultados.</span><span class="sxs-lookup"><span data-stu-id="c4db9-146">Next the code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) to advance to the records in the results.</span></span> <span data-ttu-id="c4db9-147">A continuación, el código usa [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) y [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) para analizar los valores del registro.</span><span class="sxs-lookup"><span data-stu-id="c4db9-147">Then the code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) to parse the values in the record.</span></span>

<span data-ttu-id="c4db9-148">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-148">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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


## <a name="update-data"></a><span data-ttu-id="c4db9-149">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="c4db9-149">Update data</span></span>
<span data-ttu-id="c4db9-150">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-150">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="c4db9-151">El código usa la clase NpgsqlCommand con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) para establecer una conexión a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4db9-151">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="c4db9-152">A continuación, el código usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), establece la propiedad CommandText y llama al método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-152">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="c4db9-153">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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


## <a name="delete-data"></a><span data-ttu-id="c4db9-154">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="c4db9-154">Delete data</span></span>
<span data-ttu-id="c4db9-155">Use el código siguiente para conectarse y leer los datos mediante la instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-155">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="c4db9-156">El código usa la clase NpgsqlCommand con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) para establecer una conexión a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4db9-156">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="c4db9-157">A continuación, el código usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), establece la propiedad CommandText y llama al método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) para ejecutar los comandos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-157">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="c4db9-158">Reemplace los parámetros host, dbname, user y password por los valores especificados al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4db9-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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

## <a name="next-steps"></a><span data-ttu-id="c4db9-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4db9-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c4db9-160">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="c4db9-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
