---
title: aaaUse .NET Core tooquery base de datos de SQL de Azure | Documentos de Microsoft
description: "Este tema muestra cómo toouse .NET Core toocreate un programa que conecta tooan base de datos de SQL Azure y realizar consultas sobre él mediante instrucciones Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a><span data-ttu-id="0fc3b-103">Usar .NET Core (C#) tooquery una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0fc3b-103">Use .NET Core (C#) tooquery an Azure SQL database</span></span>

<span data-ttu-id="0fc3b-104">Este tutorial de inicio rápido se muestra cómo toouse [.NET Core](https://www.microsoft.com/net/) en Windows/Linux/macOS toocreate C# programa tooconnect tooan SQL Azure base de datos y usar datos de tooquery de instrucciones de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-104">This quick start tutorial demonstrates how toouse [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS toocreate a C# program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fc3b-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0fc3b-105">Prerequisites</span></span>

<span data-ttu-id="0fc3b-106">toocomplete rápida de este tutorial de inicio, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="0fc3b-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="0fc3b-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-107">An Azure SQL database.</span></span> <span data-ttu-id="0fc3b-108">Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="0fc3b-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="0fc3b-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0fc3b-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="0fc3b-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="0fc3b-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="0fc3b-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fc3b-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="0fc3b-112">A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="0fc3b-113">Ha instalado [.NET Core para su sistema operativo](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="0fc3b-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="0fc3b-114">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="0fc3b-114">SQL server connection information</span></span>

<span data-ttu-id="0fc3b-115">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="0fc3b-116">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="0fc3b-117">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0fc3b-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0fc3b-118">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="0fc3b-119">En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="0fc3b-120">Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="0fc3b-122">Si olvida la información de inicio de sesión del servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="0fc3b-123">Puede restablecer la contraseña de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="0fc3b-124">Haga clic en **Mostrar las cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="0fc3b-125">Hola de revisión completa **ADO.NET** cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Cadena de conexión ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="0fc3b-127">Debe tener una regla de firewall en su lugar para la dirección IP pública de hello del equipo de hello en el que realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="0fc3b-128">Si se encuentran en un equipo diferente o tiene una dirección IP pública diferentes, cree un [regla de firewall de nivel de servidor mediante Hola portal de Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="0fc3b-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="0fc3b-129">Creación de un nuevo proyecto de .NET</span><span class="sxs-lookup"><span data-stu-id="0fc3b-129">Create a new .NET project</span></span>

1. <span data-ttu-id="0fc3b-130">Abra un símbolo del sistema y cree una carpeta denominada *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="0fc3b-131">Desplazarse por las carpetas de toohello que creó y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="0fc3b-131">Navigate toohello folder you created and run hello following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="0fc3b-132">Abra ***sqltest.csproj*** con el editor de texto y agregue System.Data.SqlClient como una dependencia con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="0fc3b-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using hello following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="0fc3b-133">Insertar la base de datos SQL de tooquery de código</span><span class="sxs-lookup"><span data-stu-id="0fc3b-133">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="0fc3b-134">En el entorno de desarrollo o en el editor de texto, abra **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="0fc3b-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="0fc3b-135">Reemplace el contenido de hello con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-135">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="0fc3b-136">Ejecutar código de hello</span><span class="sxs-lookup"><span data-stu-id="0fc3b-136">Run hello code</span></span>

1. <span data-ttu-id="0fc3b-137">En hello símbolo del sistema, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="0fc3b-137">At hello command prompt, run hello following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="0fc3b-138">Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0fc3b-138">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0fc3b-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0fc3b-139">Next steps</span></span>

- <span data-ttu-id="0fc3b-140">[Introducción a .NET Core en Windows/Linux/macOS mediante la línea de comandos de hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="0fc3b-140">[Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="0fc3b-141">Obtenga información acerca de cómo demasiado[conectarse y consultar una base de datos de SQL Azure mediante Hola .NET framework y Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="0fc3b-141">Learn how too[connect and query an Azure SQL database using hello .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="0fc3b-142">Obtenga información acerca de cómo demasiado[diseñar la primera base de datos de SQL Azure con SSMS](sql-database-design-first-database.md) o [diseñar la primera base de datos de SQL Azure mediante .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="0fc3b-142">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="0fc3b-143">Para más información acerca de. NET, consulte la [Documentación de .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="0fc3b-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
