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
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a>Base de datos de Azure para PostgreSQL: Use .NET (C#) tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure base de datos PostgreSQL mediante una aplicación de C#. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. Hello pasos en este artículo se supone que está familiarizado con el desarrollo con C#, y que tooworking nueva con la base de datos de Azure para PostgreSQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Creación de la base de datos: Azure Portal](quickstart-create-server-database-portal.md)
- [Creación de la base de datos: CLI](quickstart-create-server-database-azure-cli.md)

Además, deberá:
- Instale [.NET Framework](https://www.microsoft.com/net/download). Siga los pasos de Hola Hola vinculado artículo tooinstall .NET específicamente para la plataforma (Windows, Ubuntu Linux o Mac OS). 
- Instalar [Visual Studio](https://www.visualstudio.com/downloads/) o código tootype y edición de código de Visual Studio.
- Instale la biblioteca [Npgsql](http://www.npgsql.org/doc/index.html), tal y como se describe a continuación.

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a>Instalación de referencias de Npgsql en la solución de Visual Studio
tooconnect de hello C# tooPostgreSQL de aplicación, utilice la biblioteca ADO.NET de código abierto de hello denominado Npgsql. NuGet le ayuda a descargar y administrar fácilmente las referencias de Hola.

1. Cree una nueva solución de C# o abra una existente: 
   - En Visual Studio, cree una solución; para ello, haga clic en el menú Archivo **Nuevo** > **Proyecto**.
   - En el cuadro de diálogo nuevo proyecto de hello, expanda **plantillas** > **Visual C#**. 
   - Elija una plantilla adecuada, por ejemplo, **Aplicación de consola (.NET Core)**.

2. Usar hello Npgsql tooinstall del Administrador de paquetes de Nuget:
   - Haga clic en hello **herramientas** menú > **Administrador de paquetes de NuGet** > **Package Manager Console**.
   - Hola **Package Manager Console**, tipo`Install-Package Npgsql`
   - Hola instalar comando descargas hello Npgsql.dll y ensamblados relacionados y los agrega como dependencias de solución de Hola.

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos PostgreSQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **mypgserver 20170401**.
3. Haga clic en el nombre del servidor de hello **mypgserver 20170401**.
4. Servidor de hello seleccione **Introducción** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Azure Database for PostgreSQL: inicio de sesión del Administrador del servidor](./media/connect-csharp/1-connection-string.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="connect-create-table-and-insert-data"></a>Conexión, creación de una tabla e inserción de datos
Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL. código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión. A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) comandos de base de datos de toorun Hola. 

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

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

## <a name="read-data"></a>Lectura de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión. A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) y método [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) comandos de base de datos de toorun Hola. A continuación Hola código usa [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello registros en los resultados de Hola. A continuación, usa el código de hello [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) y [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse valores de hello en el registro de hello.

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

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


## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL. código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión. A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) comandos de base de datos de toorun Hola.

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

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


## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. 

 código de Hello usa NpgsqlCommand clase con el método [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish una tooPostgreSQL de conexión. A continuación, el código de hello usa el método [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), Establece la propiedad CommandText de Hola y llama a método [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) comandos de base de datos de toorun Hola.

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

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

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./howto-migrate-using-export-and-import.md)
