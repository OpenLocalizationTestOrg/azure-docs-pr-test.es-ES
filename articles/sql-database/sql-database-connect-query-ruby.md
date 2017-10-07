---
title: aaaUse Ruby tooquery base de datos de SQL de Azure | Documentos de Microsoft
description: "Este tema muestra cómo toouse toocreate Ruby un programa que conecta tooan base de datos de SQL Azure y consultas mediante instrucciones Transact-SQL."
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
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="e5e24-103">Usar Ruby tooquery una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e5e24-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="e5e24-104">Este tutorial de inicio rápido se muestra cómo toouse [Ruby](https://www.ruby-lang.org) toocreate un tooan de tooconnect programa SQL Azure la base de datos y usar datos de tooquery de instrucciones de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="e5e24-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5e24-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e5e24-105">Prerequisites</span></span>

<span data-ttu-id="e5e24-106">toocomplete rápida de este tutorial de inicio, asegúrese de tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="e5e24-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="e5e24-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e24-107">An Azure SQL database.</span></span> <span data-ttu-id="e5e24-108">Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="e5e24-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="e5e24-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e5e24-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="e5e24-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="e5e24-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="e5e24-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5e24-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="e5e24-112">A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="e5e24-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="e5e24-113">Ha instalado Ruby y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e5e24-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="e5e24-114">**MacOS**: instalación de Homebrew, instalación de rbenv y ruby-build, instalación de Ruby y, a continuación, instalación de FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="e5e24-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="e5e24-115">Consulte [pasos 1.2, 1.3, 1.4 y 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="e5e24-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="e5e24-116">**Ubuntu**: instalación de requisitos previos para Ruby, instalación de rbenv y ruby-build, instalación de Ruby y, a continuación, instalación de FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="e5e24-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="e5e24-117">Consulte [pasos 1.2, 1.3, 1.4 y 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="e5e24-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="e5e24-118">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="e5e24-118">SQL server connection information</span></span>

<span data-ttu-id="e5e24-119">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="e5e24-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="e5e24-120">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5e24-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="e5e24-121">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5e24-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e5e24-122">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="e5e24-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="e5e24-123">En hello **Introducción** página de la base de datos, revise el nombre del servidor de acceso completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5e24-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="e5e24-124">Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción, como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="e5e24-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="e5e24-126">Si ha olvidado la información de inicio de sesión de hello para el servidor de base de datos de SQL Azure, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5e24-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5e24-127">Debe tener una regla de firewall en su lugar para la dirección IP pública de hello del equipo de hello en el que realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e5e24-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="e5e24-128">Si se encuentran en un equipo diferente o tiene una dirección IP pública diferentes, cree un [regla de firewall de nivel de servidor mediante Hola portal de Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="e5e24-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="e5e24-129">Insertar la base de datos SQL de tooquery de código</span><span class="sxs-lookup"><span data-stu-id="e5e24-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="e5e24-130">En el editor de texto, cree un nuevo archivo, **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="e5e24-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="e5e24-131">Reemplace el contenido de hello con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="e5e24-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="e5e24-132">Ejecutar código de hello</span><span class="sxs-lookup"><span data-stu-id="e5e24-132">Run hello code</span></span>

1. <span data-ttu-id="e5e24-133">En hello símbolo del sistema, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e5e24-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="e5e24-134">Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e5e24-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e5e24-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5e24-135">Next Steps</span></span>
- [<span data-ttu-id="e5e24-136">Diseño de su primera base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="e5e24-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="e5e24-137">Repositorio de Github para TinyTDS</span><span class="sxs-lookup"><span data-stu-id="e5e24-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="e5e24-138">Informe de los problemas y realización de preguntas sobre TinyTDS</span><span class="sxs-lookup"><span data-stu-id="e5e24-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="e5e24-139">Controladores de Ruby para SQL Server</span><span class="sxs-lookup"><span data-stu-id="e5e24-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
