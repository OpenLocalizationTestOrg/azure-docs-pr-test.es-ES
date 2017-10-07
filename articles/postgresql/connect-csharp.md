---
title: Conectar tooAzure base de datos de PostgreSQL desde C# | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo código de C# (. NET) puede usar tooconnect y consultar los datos de la base de datos PostgreSQL."
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
ms.openlocfilehash: 5ba7426f8ad263193cdb208b3531da0ceff181dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="873c5-103">Base de datos de Azure para PostgreSQL: Use .NET (C#) tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="873c5-103">Azure Database for PostgreSQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="873c5-104">Este tutorial rápido muestra cómo tooconnect tooan Azure base de datos PostgreSQL mediante una aplicación de C#.</span><span class="sxs-lookup"><span data-stu-id="873c5-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="873c5-105">Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="873c5-106">Hello pasos en este artículo se supone que está familiarizado con el desarrollo con C#, y que tooworking nueva con la base de datos de Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="873c5-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="873c5-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="873c5-107">Prerequisites</span></span>
<span data-ttu-id="873c5-108">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="873c5-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="873c5-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="873c5-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="873c5-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="873c5-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="873c5-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="873c5-111">You also need to:</span></span>
- <span data-ttu-id="873c5-112">Instale [.NET Framework](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="873c5-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="873c5-113">Siga los pasos de Hola Hola vinculado artículo tooinstall .NET específicamente para la plataforma (Windows, Ubuntu Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="873c5-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="873c5-114">Instalar [Visual Studio](https://www.visualstudio.com/downloads/) o código tootype y edición de código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="873c5-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code tootype and edit code.</span></span>
- <span data-ttu-id="873c5-115">Instale la biblioteca [Npgsql](http://www.npgsql.org/doc/index.html), tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="873c5-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="873c5-116">Instalación de referencias de Npgsql en la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="873c5-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="873c5-117">tooconnect de hello C# tooPostgreSQL de aplicación, utilice la biblioteca ADO.NET de código abierto de hello denominado Npgsql.</span><span class="sxs-lookup"><span data-stu-id="873c5-117">tooconnect from hello C# application tooPostgreSQL, use hello open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="873c5-118">NuGet le ayuda a descargar y administrar fácilmente las referencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-118">NuGet helps download and manage hello references easily.</span></span>

1. <span data-ttu-id="873c5-119">Cree una nueva solución de C# o abra una existente:</span><span class="sxs-lookup"><span data-stu-id="873c5-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="873c5-120">En Visual Studio, cree una solución; para ello, haga clic en el menú Archivo **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="873c5-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="873c5-121">En el cuadro de diálogo nuevo proyecto de hello, expanda **plantillas** > **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="873c5-121">In hello New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="873c5-122">Elija una plantilla adecuada, por ejemplo, **Aplicación de consola (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="873c5-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="873c5-123">Usar hello Npgsql tooinstall del Administrador de paquetes de Nuget:</span><span class="sxs-lookup"><span data-stu-id="873c5-123">Use hello Nuget Package Manager tooinstall Npgsql:</span></span>
   - <span data-ttu-id="873c5-124">Haga clic en hello **herramientas** menú > **Administrador de paquetes de NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="873c5-124">Click hello **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="873c5-125">Hola **Package Manager Console**, tipo`Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="873c5-125">In hello **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="873c5-126">Hola instalar comando descargas hello Npgsql.dll y ensamblados relacionados y los agrega como dependencias de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-126">hello install command downloads hello Npgsql.dll and related assemblies and adds them as dependencies in hello solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="873c5-127">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="873c5-127">Get connection information</span></span>
<span data-ttu-id="873c5-128">Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="873c5-128">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="873c5-129">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="873c5-129">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="873c5-130">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="873c5-130">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="873c5-131">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="873c5-131">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="873c5-132">Haga clic en el nombre del servidor de hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="873c5-132">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="873c5-133">Servidor de hello seleccione **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="873c5-133">Select hello server's **Overview** page.</span></span> <span data-ttu-id="873c5-134">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="873c5-134">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="873c5-135">![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="873c5-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="873c5-136">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-136">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="873c5-137">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="873c5-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="873c5-138">Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL.</span><span class="sxs-lookup"><span data-stu-id="873c5-138">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="873c5-139">código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="873c5-139">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="873c5-140">A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-140">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span> 

<span data-ttu-id="873c5-141">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="873c5-141">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="873c5-142">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="873c5-142">Read data</span></span>
<span data-ttu-id="873c5-143">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="873c5-143">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="873c5-144">código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="873c5-144">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="873c5-145">A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) y método [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-145">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello database commands.</span></span> <span data-ttu-id="873c5-146">A continuación Hola código usa [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello registros en los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-146">Next hello code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="873c5-147">A continuación, usa el código de hello [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) y [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse valores de hello en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="873c5-147">Then hello code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello values in hello record.</span></span>

<span data-ttu-id="873c5-148">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="873c5-148">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="873c5-149">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="873c5-149">Update data</span></span>
<span data-ttu-id="873c5-150">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="873c5-150">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="873c5-151">código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="873c5-151">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="873c5-152">A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-152">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="873c5-153">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="873c5-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="873c5-154">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="873c5-154">Delete data</span></span>
<span data-ttu-id="873c5-155">Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="873c5-155">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="873c5-156">código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión.</span><span class="sxs-lookup"><span data-stu-id="873c5-156">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="873c5-157">A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) comandos de base de datos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="873c5-157">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="873c5-158">Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos.</span><span class="sxs-lookup"><span data-stu-id="873c5-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="873c5-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="873c5-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="873c5-160">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="873c5-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
