---
title: Uso de Java para consultar Azure SQL Database | Microsoft Docs
description: "En este tema se muestra cómo usar Java para crear un programa que se conecta a una base de datos SQL de Azure y realiza consultas mediante instrucciones Transact-SQL."
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
ms.openlocfilehash: 103b0755ab89a13297cfdc9ec72416664da8c1e9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-java-to-query-an-azure-sql-database"></a><span data-ttu-id="34893-103">Uso de Java para consultar una base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="34893-103">Use Java to query an Azure SQL database</span></span>

<span data-ttu-id="34893-104">Esta guía de introducción muestra cómo utilizar [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) para conectarse a una base de datos SQL de Azure y utilizar instrucciones Transact-SQL para consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="34893-104">This quick start demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database and then use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34893-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="34893-105">Prerequisites</span></span>

<span data-ttu-id="34893-106">Para completar este tutorial, asegúrese de cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="34893-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="34893-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="34893-107">An Azure SQL database.</span></span> <span data-ttu-id="34893-108">En esta guía de inicio rápido se utilizan como punto de partida los recursos creados en una de las siguientes guías:</span><span class="sxs-lookup"><span data-stu-id="34893-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="34893-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34893-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="34893-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="34893-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="34893-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="34893-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="34893-112">Una [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública del equipo que usa para seguir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="34893-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="34893-113">Ha instalado Java y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="34893-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="34893-114">**MacOS**: instalación de Homebrew y Java y, a continuación, instalación de Maven.</span><span class="sxs-lookup"><span data-stu-id="34893-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="34893-115">Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="34893-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="34893-116">**Ubuntu**: instalación del Kit de desarrollo de Java e instalación de Maven.</span><span class="sxs-lookup"><span data-stu-id="34893-116">**Ubuntu**:  Install the Java Development Kit, and install Maven.</span></span> <span data-ttu-id="34893-117">Consulte [pasos 1.2, 1.3 y 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="34893-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="34893-118">**Windows**: instalación del Kit de desarrollo de Java e instalación de Maven.</span><span class="sxs-lookup"><span data-stu-id="34893-118">**Windows**: Install the Java Development Kit, and Maven.</span></span> <span data-ttu-id="34893-119">Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="34893-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="34893-120">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="34893-120">SQL server connection information</span></span>

<span data-ttu-id="34893-121">Obtención de la información de conexión necesaria para conectarse a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="34893-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="34893-122">En los procedimientos siguientes, necesitará el nombre completo del servidor, el nombre de la base de datos y la información de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="34893-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="34893-123">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="34893-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="34893-124">Seleccione **Bases de datos SQL** en el menú de la izquierda y haga clic en la base de datos en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="34893-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="34893-125">En la página **Información general** de la base de datos, revise el nombre completo del servidor tal como se muestra en la siguiente imagen: puede mantener el ratón sobre el nombre del servidor para que aparezca la opción **Haga clic aquí para copiar**.</span><span class="sxs-lookup"><span data-stu-id="34893-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image: You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="34893-127">Si ha olvidado la información de inicio de sesión, vaya a la página del servidor de SQL Database para ver el nombre del administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="34893-127">If you forget your server login information, navigate to the SQL Database server page to view the server admin name.</span></span>  <span data-ttu-id="34893-128">Si es necesario, restablezca la contraseña.</span><span class="sxs-lookup"><span data-stu-id="34893-128">If necessary, reset the password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="34893-129">**Creación de un proyecto de Maven y sus dependencias**</span><span class="sxs-lookup"><span data-stu-id="34893-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="34893-130">Desde el terminal, cree un nuevo proyecto de Maven llamado **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="34893-130">From the terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="34893-131">Cuando se le solicite, escriba **Y** (Sí).</span><span class="sxs-lookup"><span data-stu-id="34893-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="34893-132">Cambie al directorio **sqltest** y abra ***pom.xml*** con el editor de texto.</span><span class="sxs-lookup"><span data-stu-id="34893-132">Change directory to **sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="34893-133">Agregue **Microsoft JDBC Driver para SQL Server** a las dependencias del proyecto mediante el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="34893-133">Add the **Microsoft JDBC Driver for SQL Server** to your project's dependencies using the following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="34893-134">También en ***pom.xml***, agregue las siguientes propiedades al proyecto.</span><span class="sxs-lookup"><span data-stu-id="34893-134">Also in ***pom.xml***, add the following properties to your project.</span></span>  <span data-ttu-id="34893-135">Si no tiene una sección de propiedades, puede agregarla después de las dependencias.</span><span class="sxs-lookup"><span data-stu-id="34893-135">If you don't have a properties section, you can add it after the dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="34893-136">Guarde y cierre el archivo ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="34893-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="34893-137">Inserción de código para consultar la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="34893-137">Insert code to query SQL database</span></span>

1. <span data-ttu-id="34893-138">Ya debe tener un archivo denominado ***App.java*** en el proyecto Maven ubicado en: ..\sqltest\src\main\java\com\sqlsamples\App.java</span><span class="sxs-lookup"><span data-stu-id="34893-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="34893-139">Abra el archivo y reemplace el contenido con el código siguiente y agregue los valores adecuados para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="34893-139">Open the file and replace its contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect to database
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

## <a name="run-the-code"></a><span data-ttu-id="34893-140">Ejecución del código</span><span class="sxs-lookup"><span data-stu-id="34893-140">Run the code</span></span>

1. <span data-ttu-id="34893-141">En el símbolo del sistema, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="34893-141">At the command prompt, run the following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="34893-142">Compruebe que se han devuelto las primeras 20 filas y, a continuación, cierre la ventana de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34893-142">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="34893-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34893-143">Next steps</span></span>
- [<span data-ttu-id="34893-144">Diseño de su primera base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="34893-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="34893-145">Controlador JDBC de Microsoft para SQL Server</span><span class="sxs-lookup"><span data-stu-id="34893-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="34893-146">Informe de los problemas y realización de preguntas</span><span class="sxs-lookup"><span data-stu-id="34893-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

