---
title: "una solución de base de datos de SQL Azure distribuidos geográficamente aaaImplement | Documentos de Microsoft"
description: "Obtenga información acerca de tooconfigure la base de datos de SQL Azure y la aplicación para tooa de conmutación por error replica la base de datos y probar la conmutación por error."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a>Implementar una base de datos distribuida geográficamente

En este tutorial, configurar una base de datos SQL de Azure y la aplicación para la región de conmutación por error tooa remoto y, a continuación, pruebe el plan de conmutación por error. Aprenderá a: 

> [!div class="checklist"]
> * Crear usuarios de base de datos y concederles permisos
> * Configurar una regla de firewall de nivel de base de datos
> * Crear un [grupo de conmutación por error de replicación geográfica](sql-database-geo-replication-overview.md)
> * Crear y compilar un tooquery de aplicación de Java una base de datos de SQL Azure
> * Obtener detalles de recuperación ante desastres

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.


## <a name="prerequisites"></a>Requisitos previos

toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

- Hola instalada más reciente [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). 
- Instancia de Azure SQL Database instalada. Este tutorial usa con un nombre de base de datos de ejemplo de Hola AdventureWorksLT **mySampleDatabase** de una de estas guías de inicio rápidos:

   - [Creación de la base de datos: Azure Portal](sql-database-get-started-portal.md)
   - [Creación de la base de datos: CLI](sql-database-get-started-cli.md)
   - [Creación de la base de datos: PowerShell](sql-database-get-started-powershell.md)

- Ha identificado una tooexecute método SQL secuencias de comandos en la base de datos, puede usar uno de hello siguientes herramientas de consulta:
   - editor de consultas de Hola Hola [portal de Azure](https://portal.azure.com). Para obtener más información sobre cómo utilizar el editor de consultas de hello en hello portal de Azure, consulte [conectar y consulta mediante el Editor de consultas](sql-database-get-started-portal.md#query-the-sql-database).
   - versión más reciente de Hola de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), que es un entorno integrado para administrar cualquier infraestructura SQL, desde SQL Server tooSQL base de datos de Microsoft Windows.
   - versión más reciente de Hola de [código de Visual Studio](https://code.visualstudio.com/docs), que es un editor de código gráfica para Linux, Mac OS, y Windows que admita extensiones, incluidas Hola [mssql extensión](https://aka.ms/mssql-marketplace) para realizar consultas en Microsoft SQL Server , Base de datos SQL azure y almacenamiento de datos SQL. Para más información sobre el empleo de esta herramienta con Azure SQL Database, vea [Connect and query with VS Code](sql-database-connect-query-vscode.md) (Conectar y consultar con VS Code). 

## <a name="create-database-users-and-grant-permissions"></a>Crear usuarios de base de datos y concederles permisos

Conectar tooyour base de datos y crear cuentas de usuario mediante uno de hello siguientes herramientas de consulta:

- editor de consultas de Hola Hola portal de Azure
- SQL Server Management Studio
- Visual Studio Code

Estas cuentas de usuario automáticamente replican servidor secundario tooyour (y mantenerse sincronizado). toouse SQL Server Management Studio o código de Visual Studio, deberá tooconfigure una regla de firewall que se conecta desde un cliente en una dirección IP para el que todavía no se ha configurado un servidor de seguridad. Para consultar los pasos detallados, vea [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) (Crear una regla de firewall de nivel de servidor).

- En una ventana de consulta, ejecute hello después consulta toocreate dos cuentas de usuario en la base de datos. Esta secuencia de comandos concede **db_owner** permisos toohello **app_admin** cuenta y concede **seleccione** y **actualización** toohello de permisos **app_user** cuenta. 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a>Creación de firewall de nivel de base de datos

Cree una [regla de firewall de nivel de base de datos](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) para la base de datos SQL. Esta regla de firewall de nivel de base de datos replica automáticamente toohello servidor secundario que creará en este tutorial. Para simplificar el trabajo (en este tutorial), utilice Hola de dirección IP pública del equipo de hello en el que se va a realizar pasos de hello en este tutorial. dirección IP de hello toodetermine utilizada para la regla de firewall de nivel de servidor de hello para el equipo actual, vea [crear un firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).  

- En la ventana de consulta abierta, reemplace consulta anterior Hola con hello después de consulta, reemplazando las direcciones IP Hola con las direcciones IP de hello adecuadas para su entorno.  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a>Crear un grupo de conmutación por error automático de replicación geográfica activa 

Uso de PowerShell de Azure, cree un [grupo de conmutación por error de replicación geográfica activa automáticamente](sql-database-geo-replication-overview.md) entre el servidor de SQL Azure y la nueva Hola existente vacío de servidor de SQL Azure en una región de Azure y, a continuación, agregue el grupo de conmutación por error de toohello de base de datos de ejemplo.

> [!IMPORTANT]
> Estos cmdlets necesitan Azure PowerShell 4.0. [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. Rellenar las variables para los scripts de PowerShell con valores de hello para el servidor existente y la base de datos de ejemplo y proporcionar un valor único global para el nombre del grupo de conmutación por error.

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. Cree un servidor de copia de seguridad vacío en la región de conmutación por error.

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. Crear un grupo de conmutación por error entre dos servidores de Hola.

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. Agregue el grupo de conmutación por error de toohello de base de datos.

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a>Instalación del software de Java

Hola pasos de esta sección se supone que está familiarizado con el desarrollo de Java de uso y están tooworking nueva con la base de datos de SQL Azure. 

### <a name="mac-os"></a>**Mac OS**
Abra su terminal y desplácese directorio tooa donde tiene previsto crear el proyecto de Java. Instalar **brew** y **Maven** escribiendo Hola siguientes comandos: 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

Para obtener instrucciones detalladas sobre cómo instalar y configurar el entorno de Java y Maven, vaya hello [compilar una aplicación mediante SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), seleccione **Java**, seleccione **MacOS**y, a continuación, siga Hola instrucciones detalladas para configurar Java y Maven en el paso 1.2 y 1.3.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Abra su terminal y desplácese directorio tooa donde tiene previsto crear el proyecto de Java. Instalar **Maven** escribiendo Hola siguientes comandos:

```bash
sudo apt-get install maven
```

Para obtener instrucciones detalladas sobre cómo instalar y configurar el entorno de Java y Maven, vaya hello [compilar una aplicación mediante SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), seleccione **Java**, seleccione **Ubuntu**y, a continuación, siga Hola instrucciones detalladas para configurar Java y Maven en el paso 1.2, 1.3 y 1.4.

### <a name="windows"></a>**Windows**
Instalar [Maven](https://maven.apache.org/download.cgi) con instalador oficial de Hola. Utilice a Maven toohelp administrar dependencias, compilar, probar y ejecutar el proyecto de Java. Para obtener instrucciones detalladas sobre cómo instalar y configurar el entorno de Java y Maven, vaya hello [compilar una aplicación mediante SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), seleccione **Java**, seleccione Windows y, a continuación, siga Hola instrucciones detalladas para configuración de Java y Maven en el paso 1.2 y 1.3.

## <a name="create-sqldbsample-project"></a>Crear proyecto SqlDbSample

1. En la consola de comandos de hello (por ejemplo, intensiva de errores), cree un proyecto de Maven. 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. Escriba **Y** y haga clic en **Entrar**.
3. Cambie el directorio al proyecto recién creado.

   ```bash
   cd SqlDbSamples
   ```

4. Con su editor favorito, abra el archivo pom.xml de hello en la carpeta del proyecto. 

5. Agregar hello controlador JDBC de Microsoft para proyectos de Maven de tooyour de dependencia de SQL Server, abra el editor de texto y copiar y pegar Hola siguiendo las líneas en el archivo pom.xml. No sobrescribir los valores existentes de hello rellenados en el archivo hello. Hola dependencia JDBC se debe pegar dentro de hello sección "dependencias" más grande ().   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. Especificar versión de Hola del proyecto de Java toocompile hello en agregando Hola después de sección "propiedades" en el archivo de hello pom.xml después de la sección "dependencias" de Hola. 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. Agregar siguiente Hola "crear" sección en el archivo de hello pom.xml después de hello "propiedades" sección toosupport archivos de manifiesto en archivos JAR.       

   ```xml
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
8. Guarde y cierre el archivo de hello pom.xml.
9. Abra el archivo de hello App.java (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) y reemplace el contenido de hello con hello después de contenido. Sustituir el nombre de grupo de conmutación por error de Hola por hello para el grupo de conmutación por error. Si han cambiado los valores de hello para el nombre de la base de datos de hello, usuario o contraseña, cambie también esos valores.

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. Guarde y cierre el archivo de hello App.java.

## <a name="compile-and-run-hello-sqldbsample-project"></a>Compilar y ejecutar el proyecto de hello SqlDbSample

1. En la consola de comandos de hello, ejecute el comando de toofollowing.

   ```bash
   mvn package
   ```
2. Cuando termine, ejecute hello tras la aplicación de hello toorun comando (se ejecuta durante aproximadamente 1 hora a menos que detenga manualmente):

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a>Obtener detalles de recuperación ante desastres

1. Llame a la conmutación por error manual del grupo de conmutación por error. 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. Observar Hola resultados de la aplicación durante la conmutación por error. Se producirá un error en algunos inserciones mientras actualiza Hola memoria caché de DNS.     

3. Averigüe qué rol realiza el servidor de recuperación ante desastres.

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. Conmutación por recuperación.

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. Observar Hola resultados de la aplicación durante la conmutación por recuperación. Se producirá un error en algunos inserciones mientras actualiza Hola memoria caché de DNS.     

6. Averigüe qué rol realiza el servidor de recuperación ante desastres.

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a>Pasos siguientes 

Para más información, vea [Grupos de conmutación por error y replicación geográfica activa](sql-database-geo-replication-overview.md).
