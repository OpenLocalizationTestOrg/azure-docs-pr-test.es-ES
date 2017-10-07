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
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a>Implementación de una aplicación SaaS multiinquilino con Azure SQL Database

Una aplicación de varios inquilinos es una aplicación hospedada en un entorno de nube y que proporciona Hola al mismo conjunto de servicios toohundreds o miles de inquilinos que no comparta ni ver los datos de todas las demás. Un ejemplo es una aplicación de SaaS que proporciona servicios tootenants en un entorno hospedado en la nube. Este modelo aísla los datos de Hola para cada inquilino y optimiza la distribución de Hola de los recursos de costo. 

Este tutorial se muestra cómo toocreate una aplicación de SaaS multiempresa con base de datos de SQL Azure.

En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Configurar un toosupport del entorno de base de datos de una aplicación de SaaS multiempresa, utilizando el modelo de base de datos por inquilino Hola
> * Crear un inquilino
> * Proporcionar una base de datos de inquilino y registrarlo en el catálogo de inquilino de Hola
> * Configurar una aplicación Java de ejemplo 
> * Acceder a bases de datos de inquilino y una aplicación de consola Java de ejemplo
> * Eliminar un inquilino

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

toocomplete Asegúrese de este tutorial, deberá asegurarse de que:

* Versión más reciente de hello instalada de hello y PowerShell [SDK más reciente de PowerShell de Azure](http://azure.microsoft.com/downloads/)

* Versión más reciente de hello instalada de [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Instalar SQL Server Management Studio, también instala la versión más reciente de Hola de SQLPackage, una utilidad de línea de comandos que puede ser utilizado tooautomate una variedad de tareas de desarrollo de base de datos.

* Hola instalado [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) hello y [más reciente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) instalados en su equipo. 

* Instale [Apache Maven](https://maven.apache.org/download.cgi). Se utilizará maven toohelp administrar dependencias, compilar, probar y ejecutar proyecto de Java de ejemplo de Hola

## <a name="set-up-data-environment"></a>Configuración del entorno de datos

Aprovisionará una base de datos por inquilino. modelo de base de datos por inquilino Hola proporciona Hola mayor grado de aislamiento entre los inquilinos, con poco coste de DevOps. costo de hello toooptimize de recursos de nube, se también va a aprovisionar las bases de datos del inquilino de hello en un grupo elástico, lo que permite toooptimize Hola precio y performance para un grupo de bases de datos. toolearn acerca de otro modelos de aprovisionamiento de la base de datos [ve aquí](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).

Siga estos pasos toocreate un servidor SQL server y un grupo elástico que va a hospedar las bases de datos de inquilino. 

1. Crear variables toostore valores que se usará en el resto de Hola de tutorial de Hola. Acceso seguro toomodify Hola IP dirección variable tooinclude a su dirección IP 
   
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
   
2. TooAzure de inicio de sesión y crear un grupo SQL server y flexible 
   
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
   
## <a name="create-tenant-catalog"></a>Creación de un catálogo de inquilino 

En una aplicación de SaaS varios inquilinos, es importante tooknow donde se almacena información para un inquilino. Habitualmente se almacena en una base de datos de catálogo. base de datos de catálogo de Hello es toohold usa una asignación entre un inquilino y una base de datos en el que se almacenan los datos de ese inquilino.  patrón básico de Hola se aplica si varios inquilinos o se utiliza una base de datos único inquilino.

Siga estos toocreate pasos una base de datos de catálogo para aplicación de SaaS de ejemplo de Hola.

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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a>Aprovisionamiento de la base de datos para "tenant1" y su registro en el catálogo de inquilino 
Usar Powershell tooprovision una base de datos para un nuevo inquilino 'inquilino 1' y registre a este inquilino en el catálogo de Hola. 

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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a>Aprovisionamiento de la base de datos para "tenant2" y su registro en el catálogo de inquilino
Usar Powershell tooprovision una base de datos para un nuevo inquilino 'tenant2' y registre a este inquilino en el catálogo de Hola. 

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

## <a name="set-up-sample-java-application"></a>Configuración de una aplicación Java de ejemplo 

1. Cree un proyecto de Maven. Escriba Hola siguiente en una ventana del símbolo del sistema:
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. Agregue esta dependencia, el nivel de lenguaje y generar archivos de manifiesto en el archivo de pom.xml toohello archivos JAR de toosupport opción:
   
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

3. Agregue los siguiente hello en el archivo de hello App.java:

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

4. Guarde el archivo hello.

5. Vaya toocommand consola y ejecutar

   ```bash
   mvn package
   ```

6. Cuando termine, ejecute hello tras la aplicación de hello toorun 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
salida de Hello tendrá un aspecto similar al siguiente si se ejecuta correctamente:

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

## <a name="delete-first-tenant"></a>Eliminación del primer inquilino 
Usar PowerShell toodelete Hola inquilino base de datos y el catálogo de entrada para el inquilino primera Hola.

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

Intente conectarse demasiado utilizando el 'inquilino 1' hello aplicación Java. Obtendrá un error que indica que no existe ese inquilino Hola.

## <a name="next-steps"></a>Pasos siguientes 

En este tutorial aprendió a:
> [!div class="checklist"]
> * Configurar un toosupport del entorno de base de datos de una aplicación de SaaS multiempresa, utilizando el modelo de base de datos por inquilino Hola
> * Crear un inquilino
> * Proporcionar una base de datos de inquilino y registrarlo en el catálogo de inquilino de Hola
> * Configurar una aplicación Java de ejemplo 
> * Acceder a bases de datos de inquilino y una aplicación de consola Java de ejemplo
> * Eliminar un inquilino

* Para ejemplos de tareas comunes de PowerShell, consulte los [ejemplos de PowerShell de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)

* Para patrones de diseño de aplicaciones SaaS multiinquilino, consulte los [patrones de diseño](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

* Para ejemplos de Java de tareas comunes de Azure, consulte el [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/)



