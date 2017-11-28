---
title: aaaUse Java tooquery base de datos de SQL de Azure | Documentos de Microsoft
description: "Este tema muestra cómo toouse Java toocreate un programa que conecta tooan base de datos de SQL Azure y consultas mediante instrucciones Transact-SQL."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a><span data-ttu-id="19932-103">Usar Java tooquery una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="19932-103">Use Java tooquery an Azure SQL database</span></span>

<span data-ttu-id="19932-104">Este inicio rápido se muestra cómo toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan SQL Azure la base de datos y, a continuación, usar datos de tooquery de instrucciones de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="19932-104">This quick start demonstrates how toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database and then use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19932-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19932-105">Prerequisites</span></span>

<span data-ttu-id="19932-106">toocomplete rápida de este tutorial de inicio, asegúrese de tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="19932-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="19932-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="19932-107">An Azure SQL database.</span></span> <span data-ttu-id="19932-108">Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="19932-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="19932-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="19932-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="19932-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="19932-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="19932-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="19932-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="19932-112">A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="19932-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="19932-113">Ha instalado Java y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="19932-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="19932-114">**MacOS**: instalación de Homebrew y Java y, a continuación, instalación de Maven.</span><span class="sxs-lookup"><span data-stu-id="19932-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="19932-115">Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="19932-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="19932-116">**Ubuntu**: instalar Hola Kit de desarrollo de Java y Maven.</span><span class="sxs-lookup"><span data-stu-id="19932-116">**Ubuntu**:  Install hello Java Development Kit, and install Maven.</span></span> <span data-ttu-id="19932-117">Consulte [pasos 1.2, 1.3 y 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="19932-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="19932-118">**Windows**: instalar Hola Kit de desarrollo de Java y Maven.</span><span class="sxs-lookup"><span data-stu-id="19932-118">**Windows**: Install hello Java Development Kit, and Maven.</span></span> <span data-ttu-id="19932-119">Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="19932-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="19932-120">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="19932-120">SQL server connection information</span></span>

<span data-ttu-id="19932-121">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="19932-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="19932-122">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="19932-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="19932-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="19932-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="19932-124">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="19932-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="19932-125">En hello **Introducción** página para la base de datos, revise el nombre del servidor de acceso completa de hello como se muestra en hello después de la imagen: puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.</span><span class="sxs-lookup"><span data-stu-id="19932-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image: You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="19932-127">Si olvida su información de inicio de sesión de servidor, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="19932-127">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span>  <span data-ttu-id="19932-128">Si es necesario, Hola de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="19932-128">If necessary, reset hello password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="19932-129">**Creación de un proyecto de Maven y sus dependencias**</span><span class="sxs-lookup"><span data-stu-id="19932-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="19932-130">De hello terminal, cree un nuevo proyecto de Maven llama **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="19932-130">From hello terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="19932-131">Cuando se le solicite, escriba **Y** (Sí).</span><span class="sxs-lookup"><span data-stu-id="19932-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="19932-132">Cambie el directorio demasiado**sqltest** y abra ***pom.xml*** con su editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="19932-132">Change directory too**sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="19932-133">Agregar hello **Microsoft JDBC Driver para SQL Server** Hola dependencias del proyecto tooyour mediante código siguiente:</span><span class="sxs-lookup"><span data-stu-id="19932-133">Add hello **Microsoft JDBC Driver for SQL Server** tooyour project's dependencies using hello following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="19932-134">También en ***pom.xml***, agregar Hola después proyecto tooyour de propiedades.</span><span class="sxs-lookup"><span data-stu-id="19932-134">Also in ***pom.xml***, add hello following properties tooyour project.</span></span>  <span data-ttu-id="19932-135">Si no tiene una sección de propiedades, puede agregarlo después de las dependencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="19932-135">If you don't have a properties section, you can add it after hello dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="19932-136">Guarde y cierre el archivo ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="19932-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="19932-137">Insertar la base de datos SQL de tooquery de código</span><span class="sxs-lookup"><span data-stu-id="19932-137">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="19932-138">Ya debe tener un archivo denominado ***App.java*** en el proyecto Maven ubicado en: ..\sqltest\src\main\java\com\sqlsamples\App.java</span><span class="sxs-lookup"><span data-stu-id="19932-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="19932-139">Abra el archivo hello y reemplazar su contenido con siguiente Hola de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="19932-139">Open hello file and replace its contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a><span data-ttu-id="19932-140">Ejecutar código de hello</span><span class="sxs-lookup"><span data-stu-id="19932-140">Run hello code</span></span>

1. <span data-ttu-id="19932-141">En hello símbolo del sistema, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="19932-141">At hello command prompt, run hello following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="19932-142">Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="19932-142">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="19932-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19932-143">Next steps</span></span>
- [<span data-ttu-id="19932-144">Diseño de su primera base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="19932-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="19932-145">Controlador JDBC de Microsoft para SQL Server</span><span class="sxs-lookup"><span data-stu-id="19932-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="19932-146">Informe de los problemas y realización de preguntas</span><span class="sxs-lookup"><span data-stu-id="19932-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

