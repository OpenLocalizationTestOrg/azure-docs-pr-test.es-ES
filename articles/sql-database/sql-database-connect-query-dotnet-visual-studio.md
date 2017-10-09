---
title: aaaUse Visual Studio y .NET tooquery base de datos de SQL de Azure | Documentos de Microsoft
description: "Este tema muestra cómo toouse Visual Studio toocreate un programa que conecta tooan base de datos de SQL Azure y consultas mediante instrucciones Transact-SQL."
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
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a><span data-ttu-id="95d55-103">Usar .NET (C#) con Visual Studio tooconnect y consultar una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="95d55-103">Use .NET (C#) with Visual Studio tooconnect and query an Azure SQL database</span></span>

<span data-ttu-id="95d55-104">Este tutorial de inicio rápido se muestra cómo hello toouse [.NET framework](https://www.microsoft.com/net/) toocreate C# del programa con la base de datos de SQL Azure de Visual Studio tooconnect tooan y usar datos de tooquery de instrucciones de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="95d55-104">This quick start tutorial demonstrates how toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate a C# program with Visual Studio tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95d55-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="95d55-105">Prerequisites</span></span>

<span data-ttu-id="95d55-106">toocomplete rápida de este tutorial de inicio, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="95d55-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="95d55-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="95d55-107">An Azure SQL database.</span></span> <span data-ttu-id="95d55-108">Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="95d55-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="95d55-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="95d55-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="95d55-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="95d55-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="95d55-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="95d55-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="95d55-112">A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="95d55-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="95d55-113">Una instalación de [Visual Studio Community 2017, Visual Studio Professional 2017 o Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="95d55-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="95d55-114">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="95d55-114">SQL server connection information</span></span>

<span data-ttu-id="95d55-115">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="95d55-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="95d55-116">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="95d55-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="95d55-117">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="95d55-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="95d55-118">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="95d55-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="95d55-119">En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="95d55-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="95d55-120">Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.</span><span class="sxs-lookup"><span data-stu-id="95d55-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="95d55-122">Si olvida la información de inicio de sesión del servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="95d55-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="95d55-123">Puede restablecer la contraseña de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="95d55-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="95d55-124">Haga clic en **Mostrar las cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="95d55-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="95d55-125">Hola de revisión completa **ADO.NET** cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="95d55-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Cadena de conexión ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="95d55-127">Debe tener una regla de firewall en su lugar para la dirección IP pública de hello del equipo de hello en el que realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="95d55-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="95d55-128">Si se encuentran en un equipo diferente o tiene una dirección IP pública diferentes, cree un [regla de firewall de nivel de servidor mediante Hola portal de Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="95d55-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="95d55-129">Creación de un nuevo proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95d55-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="95d55-130">En Visual Studio, seleccione **Archivo**, **Nuevo**, **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="95d55-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="95d55-131">Hola **nuevo proyecto** cuadro de diálogo y expanda **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="95d55-131">In hello **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="95d55-132">Seleccione **aplicación de consola** y escriba *sqltest* como nombre de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="95d55-132">Select **Console App** and enter *sqltest* for hello project name.</span></span>
4. <span data-ttu-id="95d55-133">Haga clic en **Aceptar** toocreate y Hola abrir nuevo proyecto en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95d55-133">Click **OK** toocreate and open hello new project in Visual Studio</span></span>
4. <span data-ttu-id="95d55-134">En el Explorador de soluciones, haga clic con el botón derecho en **sqltest** y haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="95d55-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="95d55-135">En hello **examinar**, busque ```System.Data.SqlClient``` y, cuando se encuentra, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="95d55-135">On hello **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="95d55-136">Hola **System.Data.SqlClient** página, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="95d55-136">In hello **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="95d55-137">Cuando se haya completado la instalación de hello, revise los cambios de hello y, a continuación, haga clic en **Aceptar** tooclose hello **vista previa** ventana.</span><span class="sxs-lookup"><span data-stu-id="95d55-137">When hello install completes, review hello changes and then click **OK** tooclose hello **Preview** window.</span></span> 
8. <span data-ttu-id="95d55-138">Si aparece una ventana de **Aceptación de licencia**, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="95d55-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="95d55-139">Insertar la base de datos SQL de tooquery de código</span><span class="sxs-lookup"><span data-stu-id="95d55-139">Insert code tooquery SQL database</span></span>
1. <span data-ttu-id="95d55-140">Cambiar demasiado (o abra si es necesario) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="95d55-140">Switch too(or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="95d55-141">Reemplace el contenido de Hola de **Program.cs** con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="95d55-141">Replace hello contents of **Program.cs** with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="95d55-142">Ejecutar código de hello</span><span class="sxs-lookup"><span data-stu-id="95d55-142">Run hello code</span></span>

1. <span data-ttu-id="95d55-143">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="95d55-143">Press **F5** toorun hello application.</span></span>
2. <span data-ttu-id="95d55-144">Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="95d55-144">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95d55-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95d55-145">Next steps</span></span>

- <span data-ttu-id="95d55-146">Obtenga información acerca de cómo demasiado[conectarse y consultar una base de datos de SQL Azure mediante .NET core](sql-database-connect-query-dotnet-core.md) en Windows/Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="95d55-146">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="95d55-147">Obtenga información acerca de [Introducción a .NET Core en Windows/Linux/macOS mediante la línea de comandos de hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="95d55-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="95d55-148">Obtenga información acerca de cómo demasiado[diseñar la primera base de datos de SQL Azure con SSMS](sql-database-design-first-database.md) o [diseñar la primera base de datos de SQL Azure mediante .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="95d55-148">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="95d55-149">Para más información acerca de. NET, consulte la [Documentación de .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="95d55-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
