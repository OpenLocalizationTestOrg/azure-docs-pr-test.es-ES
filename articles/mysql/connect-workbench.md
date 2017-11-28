---
title: "Conexión a Azure Database for MySQL desde MySQL Workbench | Microsoft Docs"
description: "En esta guía de inicio rápido se proporcionan los pasos para usar MySQL Workbench para conectarse a Azure Database for MySQL y consultar datos en este servicio."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a><span data-ttu-id="ed95f-103">Azure Database for MySQL: uso de MySQL Workbench para conectarse y consultar datos</span><span class="sxs-lookup"><span data-stu-id="ed95f-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span></span>
<span data-ttu-id="ed95f-104">En esta guía de inicio rápido se muestra cómo conectarse a Azure Database for MySQL mediante la aplicación MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="ed95f-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ed95f-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ed95f-105">Prerequisites</span></span>
<span data-ttu-id="ed95f-106">En este tutorial rápido se usan como punto de partida los recursos creados en una de estas guías:</span><span class="sxs-lookup"><span data-stu-id="ed95f-106">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="ed95f-107">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="ed95f-107">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="ed95f-108">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="ed95f-108">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-mysql-workbench"></a><span data-ttu-id="ed95f-109">Instalación de MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="ed95f-109">Install MySQL Workbench</span></span>
<span data-ttu-id="ed95f-110">Descargue e instale MySQL Workbench en el equipo desde [el sitio web de MySQL](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="ed95f-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="ed95f-111">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="ed95f-111">Get connection information</span></span>
<span data-ttu-id="ed95f-112">Obtenga la información de conexión necesaria para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed95f-112">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="ed95f-113">Necesitará el nombre completo del servidor y las credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ed95f-113">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ed95f-114">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ed95f-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="ed95f-115">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor que ha creado, por ejemplo, **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="ed95f-115">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="ed95f-116">Haga clic en el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="ed95f-116">Click the server name.</span></span>

4. <span data-ttu-id="ed95f-117">Seleccione la página **Propiedades** del servidor.</span><span class="sxs-lookup"><span data-stu-id="ed95f-117">Select the server's **Properties** page.</span></span> <span data-ttu-id="ed95f-118">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="ed95f-118">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Nombre del servidor de Azure Database for MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="ed95f-120">Si olvida la información de inicio de sesión del servidor, navegue hasta la página **Información general** para ver el nombre de inicio de sesión del administrador del servidor y, si es necesario, restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="ed95f-120">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-to-the-server-using-mysql-workbench"></a><span data-ttu-id="ed95f-121">Conexión al servidor con MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="ed95f-121">Connect to the server using MySQL Workbench</span></span> 
<span data-ttu-id="ed95f-122">Para conectarse al servidor Azure MySQL mediante la herramienta MySQL Workbench de la GUI:</span><span class="sxs-lookup"><span data-stu-id="ed95f-122">To connect to Azure MySQL server using the GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="ed95f-123">Inicie la aplicación MySQL Workbench en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ed95f-123">Launch the MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="ed95f-124">En el cuadro de diálogo **Setup New Connection** (Establecer nueva conexión), escriba la siguiente información en la pestaña **Parámetros**:</span><span class="sxs-lookup"><span data-stu-id="ed95f-124">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span></span>

    ![Configuración de una conexión nueva](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="ed95f-126">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="ed95f-126">**Setting**</span></span> | <span data-ttu-id="ed95f-127">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="ed95f-127">**Suggested value**</span></span> | <span data-ttu-id="ed95f-128">**Descripción del campo**</span><span class="sxs-lookup"><span data-stu-id="ed95f-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="ed95f-129">Nombre de la conexión</span><span class="sxs-lookup"><span data-stu-id="ed95f-129">Connection Name</span></span> | <span data-ttu-id="ed95f-130">Conexión de demostración</span><span class="sxs-lookup"><span data-stu-id="ed95f-130">Demo Connection</span></span> | <span data-ttu-id="ed95f-131">Especifique una etiqueta para esta conexión.</span><span class="sxs-lookup"><span data-stu-id="ed95f-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="ed95f-132">Método de conexión</span><span class="sxs-lookup"><span data-stu-id="ed95f-132">Connection Method</span></span> | <span data-ttu-id="ed95f-133">Estándar (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="ed95f-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="ed95f-134">Estándar (TCP/IP) es suficiente.</span><span class="sxs-lookup"><span data-stu-id="ed95f-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="ed95f-135">Nombre de host.</span><span class="sxs-lookup"><span data-stu-id="ed95f-135">Hostname</span></span> | <span data-ttu-id="ed95f-136">*nombre del servidor*</span><span class="sxs-lookup"><span data-stu-id="ed95f-136">*server name*</span></span> | <span data-ttu-id="ed95f-137">Especifique el valor de nombre de servidor que se usó cuando creó el servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed95f-137">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ed95f-138">El servidor de ejemplo que se muestra es myserver4demo.mysql.database.azure.com. Use el nombre de dominio completo (\*.mysql.database.azure.com) tal como se muestra en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ed95f-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span></span> <span data-ttu-id="ed95f-139">Siga los pasos de la sección anterior para obtener la información de conexión si no recuerda el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="ed95f-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="ed95f-140">Port</span><span class="sxs-lookup"><span data-stu-id="ed95f-140">Port</span></span> | <span data-ttu-id="ed95f-141">3306</span><span class="sxs-lookup"><span data-stu-id="ed95f-141">3306</span></span> | <span data-ttu-id="ed95f-142">Utilice siempre el puerto 3306 para conectarse a Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed95f-142">Always use port 3306 when connecting to Azure Database for MySQL.</span></span> |
    | <span data-ttu-id="ed95f-143">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="ed95f-143">Username</span></span> |  <span data-ttu-id="ed95f-144">*nombre de inicio de sesión del administrador del servidor*</span><span class="sxs-lookup"><span data-stu-id="ed95f-144">*server admin login name*</span></span> | <span data-ttu-id="ed95f-145">Escriba el valor de nombre de inicio de sesión del administrador del servidor que se usó al crear el servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed95f-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ed95f-146">El nombre de usuario de nuestro ejemplo es myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="ed95f-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="ed95f-147">Siga los pasos de la sección anterior para obtener la información de conexión si no recuerda el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="ed95f-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span></span> <span data-ttu-id="ed95f-148">El formato es *username@servername*.</span><span class="sxs-lookup"><span data-stu-id="ed95f-148">The format is *username@servername*.</span></span>
    | <span data-ttu-id="ed95f-149">Password</span><span class="sxs-lookup"><span data-stu-id="ed95f-149">Password</span></span> | <span data-ttu-id="ed95f-150">la contraseña</span><span class="sxs-lookup"><span data-stu-id="ed95f-150">your password</span></span> | <span data-ttu-id="ed95f-151">Haga clic en el botón **Store in Vault...** (Almacenar en el almacén) para guardar la contraseña.</span><span class="sxs-lookup"><span data-stu-id="ed95f-151">Click **Store in Vault...** button to save the password.</span></span> |

3.   <span data-ttu-id="ed95f-152">Haga clic en **Probar conexión** para probar si todos los parámetros están configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="ed95f-152">Click **Test Connection** to test if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="ed95f-153">Haga clic en **Aceptar** para guardar la conexión.</span><span class="sxs-lookup"><span data-stu-id="ed95f-153">Click **OK** to save the connection.</span></span> 

5.   <span data-ttu-id="ed95f-154">En la lista de **conexiones de MySQL**, haga clic en el icono que corresponde al servidor y espere que se establezca la conexión.</span><span class="sxs-lookup"><span data-stu-id="ed95f-154">In the listing of **MySQL Connections**, click the tile corresponding to your server and wait for the connection to be established.</span></span>

6.   <span data-ttu-id="ed95f-155">Una pestaña SQL nueva se abre con un editor en blanco en el que puede escribir las consultas.</span><span class="sxs-lookup"><span data-stu-id="ed95f-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed95f-156">De forma predeterminada, la seguridad de conexión SSL es necesaria y se aplica al servidor de Azure Database para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed95f-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="ed95f-157">Normalmente no se necesita ninguna configuración adicional con certificados SSL para que MySQL Workbench se conecte al servidor.</span><span class="sxs-lookup"><span data-stu-id="ed95f-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server.</span></span> <span data-ttu-id="ed95f-158">Para más información sobre SSL, vea [Configuración de la conectividad SSL en la aplicación para conectarse de forma segura a Azure Database for MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ed95f-158">For more information on SSL, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="ed95f-159">Si necesita deshabilitar SSL, visite Azure Portal y haga clic en la página Seguridad de la conexión para deshabilitar el botón de alternancia Aplicar conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="ed95f-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="ed95f-160">Creación de una tabla, inserción de datos, lectura de datos, actualización de datos, eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="ed95f-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="ed95f-161">Copie y pegue el código SQL de ejemplo en una pestaña SQL en blanco para mostrar algunos datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ed95f-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span></span>

    <span data-ttu-id="ed95f-162">Este código crea una base de datos vacía llamada quickstartdb y luego crea una tabla de ejemplo llamada inventario.</span><span class="sxs-lookup"><span data-stu-id="ed95f-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="ed95f-163">Inserta algunas filas y luego las lee.</span><span class="sxs-lookup"><span data-stu-id="ed95f-163">It inserts some rows, then reads the rows.</span></span> <span data-ttu-id="ed95f-164">Cambia los datos con una instrucción de actualización y vuelve a leer las filas.</span><span class="sxs-lookup"><span data-stu-id="ed95f-164">It changes the data with an update statement, and reads the rows again.</span></span> <span data-ttu-id="ed95f-165">Por último, elimina una fila y vuelve a leer las filas.</span><span class="sxs-lookup"><span data-stu-id="ed95f-165">Finally it deletes a row, and reads the rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="ed95f-166">La captura de pantalla muestra un ejemplo del código SQL en SQL Workbench y el resultado una vez que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="ed95f-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span></span>
    
    ![Pestaña SQL de MySQL Workbench para ejecutar código de SQL de ejemplo](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="ed95f-168">Para ejecutar el código SQL de ejemplo, haga clic en el icono de rayo que aparece en la barra de herramientas de la pestaña **Archivo SQL**.</span><span class="sxs-lookup"><span data-stu-id="ed95f-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span></span>
3. <span data-ttu-id="ed95f-169">Observe los tres resultados en pestañas de la sección **Cuadrículas de resultados** del centro de la página.</span><span class="sxs-lookup"><span data-stu-id="ed95f-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span></span> 
4. <span data-ttu-id="ed95f-170">Observe la lista **Salida** que se encuentra en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="ed95f-170">Notice the **Output** list at the bottom of the page.</span></span> <span data-ttu-id="ed95f-171">Se muestra el estado de cada comando.</span><span class="sxs-lookup"><span data-stu-id="ed95f-171">The status of each command is shown.</span></span> 

<span data-ttu-id="ed95f-172">Ahora está conectado a Azure Database for MySQL con MySQL Workbench y ha consultado datos mediante el lenguaje SQL.</span><span class="sxs-lookup"><span data-stu-id="ed95f-172">Now, you have connected to Azure Database for MySQL using MySQL Workbench, and have queried data using the SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed95f-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed95f-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ed95f-174">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="ed95f-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
