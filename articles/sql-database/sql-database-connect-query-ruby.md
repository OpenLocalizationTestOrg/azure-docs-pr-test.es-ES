---
title: Uso de Ruby para consultar Azure SQL Database | Microsoft Docs
description: "En este tema se muestra cómo usar Ruby para crear un programa que se conecta a una base de datos SQL de Azure y realiza consultas mediante instrucciones Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 25ff9a9cfaa5494dbb006c84e235099fe51e6545
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a><span data-ttu-id="41c60-103">Uso de Ruby para consultar una base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="41c60-103">Use Ruby to query an Azure SQL database</span></span>

<span data-ttu-id="41c60-104">Este tutorial de introducción muestra cómo usar [Ruby](https://www.ruby-lang.org) para crear un programa que se conecta a una base de datos SQL de Azure y utiliza instrucciones Transact-SQL para consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="41c60-104">This quick start tutorial demonstrates how to use [Ruby](https://www.ruby-lang.org) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41c60-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="41c60-105">Prerequisites</span></span>

<span data-ttu-id="41c60-106">Para completar este tutorial, asegúrese de cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="41c60-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="41c60-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="41c60-107">An Azure SQL database.</span></span> <span data-ttu-id="41c60-108">En esta guía de inicio rápido se utilizan como punto de partida los recursos creados en una de las siguientes guías:</span><span class="sxs-lookup"><span data-stu-id="41c60-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="41c60-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="41c60-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="41c60-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="41c60-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="41c60-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="41c60-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="41c60-112">Una [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública del equipo que usa para seguir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="41c60-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="41c60-113">Ha instalado Ruby y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="41c60-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="41c60-114">**MacOS**: instalación de Homebrew, instalación de rbenv y ruby-build, instalación de Ruby y, a continuación, instalación de FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="41c60-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="41c60-115">Consulte [pasos 1.2, 1.3, 1.4 y 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="41c60-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="41c60-116">**Ubuntu**: instalación de requisitos previos para Ruby, instalación de rbenv y ruby-build, instalación de Ruby y, a continuación, instalación de FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="41c60-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="41c60-117">Consulte [pasos 1.2, 1.3, 1.4 y 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="41c60-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="41c60-118">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="41c60-118">SQL server connection information</span></span>

<span data-ttu-id="41c60-119">Obtención de la información de conexión necesaria para conectarse a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="41c60-119">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="41c60-120">En los procedimientos siguientes, necesitará el nombre completo del servidor, el nombre de la base de datos y la información de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="41c60-120">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="41c60-121">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="41c60-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="41c60-122">Seleccione **Bases de datos SQL** en el menú de la izquierda y haga clic en la base de datos en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="41c60-122">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="41c60-123">En la página **Información general** de la base de datos, revise el nombre completo del servidor.</span><span class="sxs-lookup"><span data-stu-id="41c60-123">On the **Overview** page for your database, review the fully qualified server name.</span></span> <span data-ttu-id="41c60-124">Mantenga el puntero sobre el nombre del servidor hasta que aparezca la opción **Haga clic para copiar**, como se muestra en la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="41c60-124">You can hover over the server name to bring up the **Click to copy** option, as shown in the following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="41c60-126">Si ha olvidado la información de inicio de sesión para el servidor de Azure SQL Database, navegue a la página del servidor de SQL Database para ver el nombre del Administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="41c60-126">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41c60-127">Debe tener una regla de firewall activa para la dirección IP pública del equipo en el que sigue este tutorial.</span><span class="sxs-lookup"><span data-stu-id="41c60-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="41c60-128">Si se encuentra en un equipo diferente o tiene una dirección IP pública diferente, cree una [regla de firewall de nivel de servidor mediante Azure Portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="41c60-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="41c60-129">Inserción de código para consultar la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="41c60-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="41c60-130">En el editor de texto, cree un nuevo archivo, **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="41c60-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="41c60-131">Reemplace el contenido con el código siguiente y agregue los valores adecuados para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="41c60-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-the-code"></a><span data-ttu-id="41c60-132">Ejecución del código</span><span class="sxs-lookup"><span data-stu-id="41c60-132">Run the code</span></span>

1. <span data-ttu-id="41c60-133">En el símbolo del sistema, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="41c60-133">At the command prompt, run the following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="41c60-134">Compruebe que se han devuelto las primeras 20 filas y, a continuación, cierre la ventana de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c60-134">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="41c60-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41c60-135">Next Steps</span></span>
- [<span data-ttu-id="41c60-136">Diseño de su primera base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="41c60-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="41c60-137">Repositorio de Github para TinyTDS</span><span class="sxs-lookup"><span data-stu-id="41c60-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="41c60-138">Informe de los problemas y realización de preguntas sobre TinyTDS</span><span class="sxs-lookup"><span data-stu-id="41c60-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="41c60-139">Controladores de Ruby para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41c60-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
