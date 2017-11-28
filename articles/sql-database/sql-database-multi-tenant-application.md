---
title: "aplicación de SaaS aaaImplement multiempresa con base de datos de SQL de Azure | Documentos de Microsoft"
description: "Implementación de aplicaciones SaaS multiinquilino con Azure SQL Database."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="e205c-103">Implementación de una aplicación SaaS multiinquilino con Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e205c-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="e205c-104">Una aplicación de varios inquilinos es una aplicación hospedada en un entorno de nube y que proporciona Hola al mismo conjunto de servicios toohundreds o miles de inquilinos que no comparta ni ver los datos de todas las demás.</span><span class="sxs-lookup"><span data-stu-id="e205c-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="e205c-105">Un ejemplo es una aplicación de SaaS que proporciona servicios tootenants en un entorno hospedado en la nube.</span><span class="sxs-lookup"><span data-stu-id="e205c-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="e205c-106">Este modelo aísla los datos de Hola para cada inquilino y optimiza la distribución de Hola de los recursos de costo.</span><span class="sxs-lookup"><span data-stu-id="e205c-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="e205c-107">Este tutorial se muestra cómo toocreate una aplicación de SaaS multiempresa con base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e205c-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="e205c-108">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="e205c-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e205c-109">Configurar un toosupport del entorno de base de datos de una aplicación de SaaS multiempresa, utilizando el modelo de base de datos por inquilino Hola</span><span class="sxs-lookup"><span data-stu-id="e205c-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="e205c-110">Crear un inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="e205c-111">Proporcionar una base de datos de inquilino y registrarlo en el catálogo de inquilino de Hola</span><span class="sxs-lookup"><span data-stu-id="e205c-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="e205c-112">Configurar una aplicación Java de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e205c-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="e205c-113">Acceder a bases de datos de inquilino y una aplicación de consola Java de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e205c-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="e205c-114">Eliminar un inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-114">Delete a tenant</span></span>

<span data-ttu-id="e205c-115">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="e205c-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e205c-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e205c-116">Prerequisites</span></span>

<span data-ttu-id="e205c-117">toocomplete Asegúrese de este tutorial, deberá asegurarse de que:</span><span class="sxs-lookup"><span data-stu-id="e205c-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="e205c-118">Versión más reciente de hello instalada de hello y PowerShell [SDK más reciente de PowerShell de Azure](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e205c-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="e205c-119">Versión más reciente de hello instalada de [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="e205c-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="e205c-120">Instalar SQL Server Management Studio, también instala la versión más reciente de Hola de SQLPackage, una utilidad de línea de comandos que puede ser utilizado tooautomate una variedad de tareas de desarrollo de base de datos.</span><span class="sxs-lookup"><span data-stu-id="e205c-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="e205c-121">Hola instalado [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) hello y [más reciente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) instalados en su equipo.</span><span class="sxs-lookup"><span data-stu-id="e205c-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="e205c-122">Instale [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="e205c-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="e205c-123">Se utilizará maven toohelp administrar dependencias, compilar, probar y ejecutar proyecto de Java de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="e205c-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="e205c-124">Configuración del entorno de datos</span><span class="sxs-lookup"><span data-stu-id="e205c-124">Set up data environment</span></span>

<span data-ttu-id="e205c-125">Aprovisionará una base de datos por inquilino.</span><span class="sxs-lookup"><span data-stu-id="e205c-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="e205c-126">modelo de base de datos por inquilino Hola proporciona Hola mayor grado de aislamiento entre los inquilinos, con poco coste de DevOps.</span><span class="sxs-lookup"><span data-stu-id="e205c-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="e205c-127">costo de hello toooptimize de recursos de nube, se también va a aprovisionar las bases de datos del inquilino de hello en un grupo elástico, lo que permite toooptimize Hola precio y performance para un grupo de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="e205c-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="e205c-128">toolearn acerca de otro modelos de aprovisionamiento de la base de datos [ve aquí](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="e205c-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="e205c-129">Siga estos pasos toocreate un servidor SQL server y un grupo elástico que va a hospedar las bases de datos de inquilino.</span><span class="sxs-lookup"><span data-stu-id="e205c-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="e205c-130">Crear variables toostore valores que se usará en el resto de Hola de tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="e205c-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="e205c-131">Acceso seguro toomodify Hola IP dirección variable tooinclude a su dirección IP</span><span class="sxs-lookup"><span data-stu-id="e205c-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="e205c-132">TooAzure de inicio de sesión y crear un grupo SQL server y flexible</span><span class="sxs-lookup"><span data-stu-id="e205c-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="e205c-133">Creación de un catálogo de inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-133">Create tenant catalog</span></span> 

<span data-ttu-id="e205c-134">En una aplicación de SaaS varios inquilinos, es importante tooknow donde se almacena información para un inquilino.</span><span class="sxs-lookup"><span data-stu-id="e205c-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="e205c-135">Habitualmente se almacena en una base de datos de catálogo.</span><span class="sxs-lookup"><span data-stu-id="e205c-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="e205c-136">base de datos de catálogo de Hello es toohold usa una asignación entre un inquilino y una base de datos en el que se almacenan los datos de ese inquilino.</span><span class="sxs-lookup"><span data-stu-id="e205c-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="e205c-137">patrón básico de Hola se aplica si varios inquilinos o se utiliza una base de datos único inquilino.</span><span class="sxs-lookup"><span data-stu-id="e205c-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="e205c-138">Siga estos toocreate pasos una base de datos de catálogo para aplicación de SaaS de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e205c-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="e205c-139">Aprovisionamiento de la base de datos para "tenant1" y su registro en el catálogo de inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="e205c-140">Usar Powershell tooprovision una base de datos para un nuevo inquilino 'inquilino 1' y registre a este inquilino en el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e205c-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="e205c-141">Aprovisionamiento de la base de datos para "tenant2" y su registro en el catálogo de inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="e205c-142">Usar Powershell tooprovision una base de datos para un nuevo inquilino 'tenant2' y registre a este inquilino en el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e205c-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a><span data-ttu-id="e205c-143">Configuración de una aplicación Java de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e205c-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="e205c-144">Cree un proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="e205c-144">Create a maven project.</span></span> <span data-ttu-id="e205c-145">Escriba Hola siguiente en una ventana del símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="e205c-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="e205c-146">Agregue esta dependencia, el nivel de lenguaje y generar archivos de manifiesto en el archivo de pom.xml toohello archivos JAR de toosupport opción:</span><span class="sxs-lookup"><span data-stu-id="e205c-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
   <build>
        <plugins>
           <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-jar-plugin</artifactId>
              <version>3.0.0</version>
              <configuration>
                 <archive>
                    <manifest>
                       <mainClass>com.sqldbsamples.App</mainClass>
                    </manifest>
                 </archive>
              </configuration>
           </plugin>
        </plugins>
   </build>
   ```

3. <span data-ttu-id="e205c-147">Agregue los siguiente hello en el archivo de hello App.java:</span><span class="sxs-lookup"><span data-stu-id="e205c-147">Add hello following into hello App.java file:</span></span>

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in hello system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. <span data-ttu-id="e205c-148">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="e205c-148">Save hello file.</span></span>

5. <span data-ttu-id="e205c-149">Vaya toocommand consola y ejecutar</span><span class="sxs-lookup"><span data-stu-id="e205c-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="e205c-150">Cuando termine, ejecute hello tras la aplicación de hello toorun</span><span class="sxs-lookup"><span data-stu-id="e205c-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="e205c-151">salida de Hello tendrá un aspecto similar al siguiente si se ejecuta correctamente:</span><span class="sxs-lookup"><span data-stu-id="e205c-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="e205c-152">Eliminación del primer inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-152">Delete first tenant</span></span> 
<span data-ttu-id="e205c-153">Usar PowerShell toodelete Hola inquilino base de datos y el catálogo de entrada para el inquilino primera Hola.</span><span class="sxs-lookup"><span data-stu-id="e205c-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

<span data-ttu-id="e205c-154">Intente conectarse demasiado utilizando el 'inquilino 1' hello aplicación Java.</span><span class="sxs-lookup"><span data-stu-id="e205c-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="e205c-155">Obtendrá un error que indica que no existe ese inquilino Hola.</span><span class="sxs-lookup"><span data-stu-id="e205c-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e205c-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e205c-156">Next steps</span></span> 

<span data-ttu-id="e205c-157">En este tutorial aprendió a:</span><span class="sxs-lookup"><span data-stu-id="e205c-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e205c-158">Configurar un toosupport del entorno de base de datos de una aplicación de SaaS multiempresa, utilizando el modelo de base de datos por inquilino Hola</span><span class="sxs-lookup"><span data-stu-id="e205c-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="e205c-159">Crear un inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="e205c-160">Proporcionar una base de datos de inquilino y registrarlo en el catálogo de inquilino de Hola</span><span class="sxs-lookup"><span data-stu-id="e205c-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="e205c-161">Configurar una aplicación Java de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e205c-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="e205c-162">Acceder a bases de datos de inquilino y una aplicación de consola Java de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e205c-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="e205c-163">Eliminar un inquilino</span><span class="sxs-lookup"><span data-stu-id="e205c-163">Delete a tenant</span></span>

* <span data-ttu-id="e205c-164">Para ejemplos de tareas comunes de PowerShell, consulte los [ejemplos de PowerShell de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="e205c-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="e205c-165">Para patrones de diseño de aplicaciones SaaS multiinquilino, consulte los [patrones de diseño](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="e205c-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="e205c-166">Para ejemplos de Java de tareas comunes de Azure, consulte el [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="e205c-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



