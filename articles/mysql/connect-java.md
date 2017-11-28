---
title: "Conexión a Azure Database for MySQL mediante Java | Microsoft Docs"
description: "En este tutorial rápido se proporciona un ejemplo de código de Java que puede usar para conectarse a una base de datos de Azure Database for MySQL y consultar datos."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: 6ffcf3b38a3d868dfa10ea2e2a9d097441387d4f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-java-to-connect-and-query-data"></a><span data-ttu-id="b73f1-103">Azure Database for MySQL: uso de Java para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="b73f1-103">Azure Database for MySQL: Use Java to connect and query data</span></span>
<span data-ttu-id="b73f1-104">En este tutorial rápido se muestra cómo conectarse a una instancia de Azure Database for MySQL mediante una aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="b73f1-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="b73f1-105">Se indica cómo usar instrucciones SQL para consultar, insertar, actualizar y eliminar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b73f1-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b73f1-106">En los pasos de este artículo se da por hecho que está familiarizado con el desarrollo mediante Java y que nunca ha utilizado Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="b73f1-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b73f1-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b73f1-107">Prerequisites</span></span>
<span data-ttu-id="b73f1-108">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="b73f1-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="b73f1-109">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="b73f1-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="b73f1-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="b73f1-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="b73f1-111">Además, deberá:</span><span class="sxs-lookup"><span data-stu-id="b73f1-111">You also need to:</span></span>
- <span data-ttu-id="b73f1-112">Descargar el controlador de JDBC [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="b73f1-112">Download the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="b73f1-113">Incluir el archivo jar de JDBC (por ejemplo, mysql-connector-java-5.1.42-bin.jar) en la ruta de clase de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b73f1-113">Include the JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="b73f1-114">Si tiene problemas con esto, consulte la documentación del entorno para conocer los detalles de ruta de clase, como [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) o [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="b73f1-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="b73f1-115">Asegurarse de que se configura la seguridad de conexión de Azure Database for MySQL con el firewall abierto y la configuración de SSL correcta conectar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b73f1-115">Ensure your Azure Database for MySQL connection security is configured with the firewall opened and SSL settings adjusted for your application to connect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b73f1-116">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="b73f1-116">Get connection information</span></span>
<span data-ttu-id="b73f1-117">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="b73f1-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="b73f1-118">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b73f1-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b73f1-119">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b73f1-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b73f1-120">En el panel izquierdo, haga clic en **Todos los recursos** y, a continuación, busque el servidor que ha creado (por ejemplo, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="b73f1-120">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="b73f1-121">Haga clic en el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="b73f1-121">Click the server name.</span></span>
4. <span data-ttu-id="b73f1-122">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="b73f1-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="b73f1-123">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="b73f1-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b73f1-124">![Nombre del servidor de Azure Database for MySQL](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b73f1-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b73f1-125">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="b73f1-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b73f1-126">Conexión, creación de una tabla e inserción de datos</span><span class="sxs-lookup"><span data-stu-id="b73f1-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="b73f1-127">Use el código siguiente para conectarse y cargar los datos mediante la función con una instrucción SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="b73f1-127">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="b73f1-128">Para la conexión a MySQL se utiliza el método [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html).</span><span class="sxs-lookup"><span data-stu-id="b73f1-128">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="b73f1-129">Los métodos [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) y execute() sirven para colocar y crear la tabla.</span><span class="sxs-lookup"><span data-stu-id="b73f1-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used to drop and create the table.</span></span> <span data-ttu-id="b73f1-130">El objeto prepareStatement sirve para generar los comandos insert, con setString() y setInt() para enlazar los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="b73f1-130">The prepareStatement object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="b73f1-131">El método executeUpdate() ejecuta el comando para insertar los valores en cada conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="b73f1-131">Method executeUpdate() runs the command for each set of parameters to insert the values.</span></span> 

<span data-ttu-id="b73f1-132">Reemplace los parámetros de host, database, user y password por los valores que especificó al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b73f1-132">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
                
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="read-data"></a><span data-ttu-id="b73f1-133">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="b73f1-133">Read data</span></span>
<span data-ttu-id="b73f1-134">Use el código siguiente para leer los datos con una instrucción SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="b73f1-134">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="b73f1-135">Para la conexión a MySQL se utiliza el método [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html).</span><span class="sxs-lookup"><span data-stu-id="b73f1-135">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="b73f1-136">Los métodos [crateStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) y executeQuery() se usan para la conexión y la ejecución de la instrucción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b73f1-136">The methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used to connect and run the select statement.</span></span> <span data-ttu-id="b73f1-137">Los resultados se procesan mediante un objeto [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html).</span><span class="sxs-lookup"><span data-stu-id="b73f1-137">The results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="b73f1-138">Reemplace los parámetros de host, database, user y password por los valores que especificó al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b73f1-138">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="b73f1-139">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="b73f1-139">Update data</span></span>
<span data-ttu-id="b73f1-140">Use el código siguiente para cambiar los datos con una instrucción SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="b73f1-140">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="b73f1-141">Para la conexión a MySQL se utiliza el método [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html).</span><span class="sxs-lookup"><span data-stu-id="b73f1-141">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="b73f1-142">Los métodos [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) y executeUpdate() se usan para la conexión y la ejecución de la instrucción update.</span><span class="sxs-lookup"><span data-stu-id="b73f1-142">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="b73f1-143">Reemplace los parámetros de host, database, user y password por los valores que especificó al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b73f1-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="b73f1-144">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="b73f1-144">Delete data</span></span>
<span data-ttu-id="b73f1-145">Use el código siguiente para quitar datos con una instrucción SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="b73f1-145">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="b73f1-146">Para la conexión a MySQL se utiliza el método [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html).</span><span class="sxs-lookup"><span data-stu-id="b73f1-146">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span>  <span data-ttu-id="b73f1-147">Los métodos [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) y executeUpdate() se usan para la conexión y la ejecución de la instrucción update.</span><span class="sxs-lookup"><span data-stu-id="b73f1-147">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="b73f1-148">Reemplace los parámetros de host, database, user y password por los valores que especificó al crear el servidor y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b73f1-148">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b73f1-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b73f1-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b73f1-150">Migre su Base de datos MySQL a Azure Database for MySQL mediante el volcado y la restauración</span><span class="sxs-lookup"><span data-stu-id="b73f1-150">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
