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
# <a name="use-java-tooquery-an-azure-sql-database"></a>Usar Java tooquery una base de datos de SQL Azure

Este inicio rápido se muestra cómo toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan SQL Azure la base de datos y, a continuación, usar datos de tooquery de instrucciones de Transact-SQL.

## <a name="prerequisites"></a>Requisitos previos

toocomplete rápida de este tutorial de inicio, asegúrese de tener Hola siguiendo los requisitos previos:

- Una base de datos SQL de Azure. Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales: 

   - [Creación de la base de datos: Azure Portal](sql-database-get-started-portal.md)
   - [Creación de la base de datos: CLI](sql-database-get-started-cli.md)
   - [Creación de la base de datos: PowerShell](sql-database-get-started-powershell.md)

- A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.

- Ha instalado Java y el software relacionado para el sistema operativo.

    - **MacOS**: instalación de Homebrew y Java y, a continuación, instalación de Maven. Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).
    - **Ubuntu**: instalar Hola Kit de desarrollo de Java y Maven. Consulte [pasos 1.2, 1.3 y 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).
    - **Windows**: instalar Hola Kit de desarrollo de Java y Maven. Consulte [pasos 1.2 y 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).    

## <a name="sql-server-connection-information"></a>Información de conexión de SQL server

Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria. Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 
3. En hello **Introducción** página para la base de datos, revise el nombre del servidor de acceso completa de hello como se muestra en hello después de la imagen: puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si olvida su información de inicio de sesión de servidor, navegue toohello base de datos de SQL server página tooview Hola administrador nombre del servidor.  Si es necesario, Hola de restablecimiento de contraseña.     

## <a name="create-maven-project-and-dependencies"></a>**Creación de un proyecto de Maven y sus dependencias**
1. De hello terminal, cree un nuevo proyecto de Maven llama **sqltest**. 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. Cuando se le solicite, escriba **Y** (Sí).
3. Cambie el directorio demasiado**sqltest** y abra ***pom.xml*** con su editor de texto que prefiera.  Agregar hello **Microsoft JDBC Driver para SQL Server** Hola dependencias del proyecto tooyour mediante código siguiente:

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. También en ***pom.xml***, agregar Hola después proyecto tooyour de propiedades.  Si no tiene una sección de propiedades, puede agregarlo después de las dependencias de Hola.

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. Guarde y cierre el archivo ***pom.xml***.

## <a name="insert-code-tooquery-sql-database"></a>Insertar la base de datos SQL de tooquery de código

1. Ya debe tener un archivo denominado ***App.java*** en el proyecto Maven ubicado en: ..\sqltest\src\main\java\com\sqlsamples\App.java

2. Abra el archivo hello y reemplazar su contenido con siguiente Hola de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.

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

## <a name="run-hello-code"></a>Ejecutar código de hello

1. En hello símbolo del sistema, ejecute hello siguientes comandos:

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.


## <a name="next-steps"></a>Pasos siguientes
- [Diseño de su primera base de datos SQL de Azure](sql-database-design-first-database.md)
- [Controlador JDBC de Microsoft para SQL Server](https://github.com/microsoft/mssql-jdbc)
- [Informe de los problemas y realización de preguntas](https://github.com/microsoft/mssql-jdbc/issues)

