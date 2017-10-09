---
title: Conectar tooAzure base de datos de MySQL desde MySQL Workbench | Documentos de Microsoft
description: "Este tutorial rápido proporciona Hola pasos toouse MySQL Workbench tooconnect y consultar datos de base de datos de Azure para MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="52304-103">Base de datos de Azure para MySQL: Use MySQL Workbench tooconnect y consultar datos</span><span class="sxs-lookup"><span data-stu-id="52304-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="52304-104">Este tutorial rápido muestra cómo tooconnect tooan base de datos de Azure para el uso de MySQL Hola aplicación MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="52304-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="52304-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52304-105">Prerequisites</span></span>
<span data-ttu-id="52304-106">Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:</span><span class="sxs-lookup"><span data-stu-id="52304-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="52304-107">[Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="52304-107">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="52304-108">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="52304-108">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-mysql-workbench"></a><span data-ttu-id="52304-109">Instalación de MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="52304-109">Install MySQL Workbench</span></span>
<span data-ttu-id="52304-110">Descargar e instalar el MySQL Workbench en el equipo de [sitio Web de MySQL de hello](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="52304-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="52304-111">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="52304-111">Get connection information</span></span>
<span data-ttu-id="52304-112">Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="52304-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="52304-113">Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.</span><span class="sxs-lookup"><span data-stu-id="52304-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="52304-114">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52304-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="52304-115">En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="52304-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="52304-116">Haga clic en el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-116">Click hello server name.</span></span>

4. <span data-ttu-id="52304-117">Servidor de hello seleccione **propiedades** página.</span><span class="sxs-lookup"><span data-stu-id="52304-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="52304-118">Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="52304-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Nombre del servidor de Azure Database for MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="52304-120">Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="52304-121">Conectar con MySQL Workbench de servidor de toohello</span><span class="sxs-lookup"><span data-stu-id="52304-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="52304-122">servidor de MySQL de tooconnect tooAzure mediante Hola GUI MySQL Workbench:</span><span class="sxs-lookup"><span data-stu-id="52304-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="52304-123">Inicie Hola aplicación MySQL Workbench en el equipo.</span><span class="sxs-lookup"><span data-stu-id="52304-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="52304-124">En **el programa de instalación nueva conexión** diálogo cuadro, escriba Hola siguiente información en hello **parámetros** ficha:</span><span class="sxs-lookup"><span data-stu-id="52304-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![Configuración de una conexión nueva](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="52304-126">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="52304-126">**Setting**</span></span> | <span data-ttu-id="52304-127">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="52304-127">**Suggested value**</span></span> | <span data-ttu-id="52304-128">**Descripción del campo**</span><span class="sxs-lookup"><span data-stu-id="52304-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="52304-129">Nombre de la conexión</span><span class="sxs-lookup"><span data-stu-id="52304-129">Connection Name</span></span> | <span data-ttu-id="52304-130">Conexión de demostración</span><span class="sxs-lookup"><span data-stu-id="52304-130">Demo Connection</span></span> | <span data-ttu-id="52304-131">Especifique una etiqueta para esta conexión.</span><span class="sxs-lookup"><span data-stu-id="52304-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="52304-132">Método de conexión</span><span class="sxs-lookup"><span data-stu-id="52304-132">Connection Method</span></span> | <span data-ttu-id="52304-133">Estándar (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="52304-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="52304-134">Estándar (TCP/IP) es suficiente.</span><span class="sxs-lookup"><span data-stu-id="52304-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="52304-135">Nombre de host.</span><span class="sxs-lookup"><span data-stu-id="52304-135">Hostname</span></span> | <span data-ttu-id="52304-136">*nombre del servidor*</span><span class="sxs-lookup"><span data-stu-id="52304-136">*server name*</span></span> | <span data-ttu-id="52304-137">Especifique el valor de nombre de servidor de Hola que se usó cuando creó Hola base de datos de Azure para MySQL anteriormente.</span><span class="sxs-lookup"><span data-stu-id="52304-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="52304-138">El servidor de ejemplo que se muestra es myserver4demo.mysql.database.azure.com. Usar el nombre de dominio completo de hello (\*. mysql.database.azure.com) tal y como se muestra en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="52304-139">Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="52304-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="52304-140">Port</span><span class="sxs-lookup"><span data-stu-id="52304-140">Port</span></span> | <span data-ttu-id="52304-141">3306</span><span class="sxs-lookup"><span data-stu-id="52304-141">3306</span></span> | <span data-ttu-id="52304-142">Utilice siempre el puerto 3306 al conectarse tooAzure base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="52304-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="52304-143">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="52304-143">Username</span></span> |  <span data-ttu-id="52304-144">*nombre de inicio de sesión del administrador del servidor*</span><span class="sxs-lookup"><span data-stu-id="52304-144">*server admin login name*</span></span> | <span data-ttu-id="52304-145">Escriba Hola server inicio de sesión nombre de usuario administrador especificó al crear Hola base de datos de Azure para MySQL anteriormente.</span><span class="sxs-lookup"><span data-stu-id="52304-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="52304-146">El nombre de usuario de nuestro ejemplo es myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="52304-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="52304-147">Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="52304-148">formato de Hello es  *username@servername* .</span><span class="sxs-lookup"><span data-stu-id="52304-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="52304-149">Password</span><span class="sxs-lookup"><span data-stu-id="52304-149">Password</span></span> | <span data-ttu-id="52304-150">la contraseña</span><span class="sxs-lookup"><span data-stu-id="52304-150">your password</span></span> | <span data-ttu-id="52304-151">Haga clic en **almacén en el almacén...**  contraseña de botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="52304-152">Haga clic en **Probar conexión** tootest si todos los parámetros están configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="52304-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="52304-153">Haga clic en **Aceptar** conexión de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="52304-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="52304-154">En la lista de Hola de **MySQL conexiones**, haga clic en servidor de hello mosaico correspondiente tooyour y espere hello toobe de conexión establecida.</span><span class="sxs-lookup"><span data-stu-id="52304-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="52304-155">Una pestaña SQL nueva se abre con un editor en blanco en el que puede escribir las consultas.</span><span class="sxs-lookup"><span data-stu-id="52304-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="52304-156">De forma predeterminada, la seguridad de conexión SSL es necesaria y se aplica al servidor de Azure Database para MySQL.</span><span class="sxs-lookup"><span data-stu-id="52304-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="52304-157">Normalmente ninguna configuración adicional con certificados SSL es necesaria para el servidor de MySQL Workbench tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="52304-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="52304-158">Para obtener más información sobre SSL, consulte [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="52304-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="52304-159">Si necesita toodisable SSL, visite el portal de Azure de Hola y haga clic en hello conexión seguridad página toodisable Hola exigir SSL conexión botón de alternancia.</span><span class="sxs-lookup"><span data-stu-id="52304-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="52304-160">Creación de una tabla, inserción de datos, lectura de datos, actualización de datos, eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="52304-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="52304-161">Copie y pegue el código de ejemplo de Hola SQL en un tooillustrate de pestaña SQL en blanco algunos datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="52304-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="52304-162">Este código crea una base de datos vacía llamada quickstartdb y luego crea una tabla de ejemplo llamada inventario.</span><span class="sxs-lookup"><span data-stu-id="52304-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="52304-163">Inserta filas, a continuación, se lee filas Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="52304-164">Cambia datos Hola con una instrucción update y lecturas Hola filas de nuevo.</span><span class="sxs-lookup"><span data-stu-id="52304-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="52304-165">Por último, se elimina una fila y lee filas Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="52304-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
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

    <span data-ttu-id="52304-166">captura de pantalla de Hello muestra un ejemplo de Hola código SQL en la salida de SQL Workbench y Hola después de que se ha ejecutado.</span><span class="sxs-lookup"><span data-stu-id="52304-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![Código de pestaña de SQL Workbench MySQL toorun ejemplo SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="52304-168">ejemplo de Hola a toorun código SQL, haga clic en icono en la barra de herramientas de Hola de Hola de rayo de hello **archivo SQL** ficha.</span><span class="sxs-lookup"><span data-stu-id="52304-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="52304-169">Tenga en cuenta Hola tres resultados con pestañas en hello **cuadrícula de resultados** sección en medio de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="52304-170">Hola aviso **salida** lista final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="52304-171">se muestra el estado de Hola de cada comando.</span><span class="sxs-lookup"><span data-stu-id="52304-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="52304-172">Ahora, ha conectado tooAzure base de datos de MySQL con MySQL Workbench y ha consultado datos mediante el lenguaje SQL Hola.</span><span class="sxs-lookup"><span data-stu-id="52304-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52304-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52304-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="52304-174">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="52304-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
