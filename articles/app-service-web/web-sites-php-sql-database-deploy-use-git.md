---
title: "Crear una aplicación web de PHP-SQL e implementarla en el Servicio de aplicaciones de Azure mediante Git"
description: "Un tutorial en el que se muestra cómo crear una aplicación web de PHP que almacena datos en Base de datos SQL de Azure y usar la implementación de Git en el Servicio de aplicaciones de Azure."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0baa3eced3824fec0907ca937c594f127a2bdf8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="a1832-103">Crear una aplicación web de PHP-SQL e implementarla en el Servicio de aplicaciones de Azure mediante Git</span><span class="sxs-lookup"><span data-stu-id="a1832-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="a1832-104">En este tutorial se muestra cómo crear una aplicación web PHP en el [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que se conecta a Base de datos SQL de Azure y cómo implementarla mediante Git.</span><span class="sxs-lookup"><span data-stu-id="a1832-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="a1832-105">En este tutorial se supone que tiene [PHP][install-php], [SQL Server Express][install-SQLExpress], [controladores de Microsoft para SQL Server para PHP](http://www.microsoft.com/download/en/details.aspx?id=20098) y [Git][install-git] instalados en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a1832-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="a1832-106">Una vez completada esta guía, tendrá una aplicación web PHP-SQL que se ejecutará en Azure.</span><span class="sxs-lookup"><span data-stu-id="a1832-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="a1832-107">Puede instalar y configurar PHP, SQL Server Express, los controladores de Microsoft para SQL Server para PHP mediante el [instalador de plataforma web de Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1832-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="a1832-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="a1832-108">You will learn:</span></span>

* <span data-ttu-id="a1832-109">Creación de una aplicación web de Azure y una base de datos SQL mediante el [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="a1832-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="a1832-110">Dado que PHP está habilitado en Aplicaciones web del Servicio de aplicaciones de forma predeterminada, no existen requisitos especiales para ejecutar el código PHP.</span><span class="sxs-lookup"><span data-stu-id="a1832-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="a1832-111">Publicar y volver a publicar la aplicación en Azure con Git.</span><span class="sxs-lookup"><span data-stu-id="a1832-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="a1832-112">Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP</span><span class="sxs-lookup"><span data-stu-id="a1832-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="a1832-113">que se hospedará en un sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1832-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="a1832-114">Captura de pantalla de la aplicación completa:</span><span class="sxs-lookup"><span data-stu-id="a1832-114">A screenshot of the completed application is below:</span></span>

![Sitio web PHP de Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a1832-116">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a1832-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a1832-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a1832-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="a1832-118">Creación de una aplicación web de Azure y configuración de la publicación Git</span><span class="sxs-lookup"><span data-stu-id="a1832-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="a1832-119">Siga estos pasos para crear una aplicación web de Azure y una base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="a1832-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="a1832-120">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a1832-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a1832-121">Abra Azure Marketplace haciendo clic en el icono **Nuevo** situado en la parte superior izquierda del panel, haga clic en **Seleccionar todo** junto a Marketplace y seleccione **Web + móvil**.</span><span class="sxs-lookup"><span data-stu-id="a1832-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="a1832-122">En Marketplace, elija **Web + móvil**.</span><span class="sxs-lookup"><span data-stu-id="a1832-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="a1832-123">Haga clic en el icono **Aplicación web + SQL** .</span><span class="sxs-lookup"><span data-stu-id="a1832-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="a1832-124">Después de leer la descripción de la aplicación web + SQL, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a1832-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="a1832-125">Haga clic en cada parte (**Grupo de recursos**, **Aplicación web**, **Base de datos** y **Suscripción**) y escriba o seleccione los valores para los campos obligatorios:</span><span class="sxs-lookup"><span data-stu-id="a1832-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="a1832-126">Escriba un nombre de URL de su elección.</span><span class="sxs-lookup"><span data-stu-id="a1832-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="a1832-127">Configuración de credenciales de servidor de bases de datos</span><span class="sxs-lookup"><span data-stu-id="a1832-127">Configure database server credentials</span></span>
   * <span data-ttu-id="a1832-128">Seleccione la región más cercana a la suya.</span><span class="sxs-lookup"><span data-stu-id="a1832-128">Select the region closest to you</span></span>
     
     ![configurar su aplicación](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="a1832-130">Cuando termine de definir la aplicación web, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a1832-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="a1832-131">Una vez creada la aplicación web, el botón **Notificaciones** emitirá el mensaje **Correcto** en color verde y la hoja del grupo de recursos se abrirá para mostrar la aplicación web y la base de datos SQL en el grupo.</span><span class="sxs-lookup"><span data-stu-id="a1832-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="a1832-132">Haga clic en el icono de la hoja del grupo de recursos para abrirla.</span><span class="sxs-lookup"><span data-stu-id="a1832-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![Grupo de recursos de la aplicación web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="a1832-134">En **Configuración**, haga clic en **Implementación continua** > **Configurar los valores obligatorios**.</span><span class="sxs-lookup"><span data-stu-id="a1832-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="a1832-135">Seleccione **Repositorio de Git local** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a1832-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![Dónde está su código fuente](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="a1832-137">Si no ha configurado antes un repositorio de Git, debe facilitar un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="a1832-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="a1832-138">Para ello, haga clic en **Configuración** > **Credenciales de implementación** en la hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a1832-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="a1832-139">En **Configuración**, haga clic en **Propiedades** para ver la dirección URL remota de Git que necesita para implementar la aplicación PHP más adelante.</span><span class="sxs-lookup"><span data-stu-id="a1832-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="a1832-140">Obtención de información de conexión de la Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a1832-140">Get SQL Database connection information</span></span>
<span data-ttu-id="a1832-141">Para conectarse a la instancia de Base de datos SQL vinculada a la aplicación web, necesitará la información de conexión que especificó al crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a1832-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="a1832-142">Para obtener la información de conexión de Base de datos SQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a1832-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="a1832-143">En la hoja del grupo de recursos, haga clic en el icono de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a1832-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="a1832-144">En la hoja de Base de datos SQL, haga clic en **Configuración** > **Propiedades** y, luego, en **Mostrar cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="a1832-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Ver las propiedades de una base de datos](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="a1832-146">En la sección **PHP** del cuadro de diálogo que aparece, anote los valores de `Server`, `SQL Database` y `User Name`.</span><span class="sxs-lookup"><span data-stu-id="a1832-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="a1832-147">Usará estos valores más adelante al publicar la aplicación web PHP en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1832-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="a1832-148">Compilación y comprobación de la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="a1832-148">Build and test your application locally</span></span>
<span data-ttu-id="a1832-149">Registration es una sencilla aplicación PHP que permite registrarse en un evento con solo proporcionar el nombre y la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="a1832-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="a1832-150">La información de los usuarios inscritos anteriormente se muestra en una tabla.</span><span class="sxs-lookup"><span data-stu-id="a1832-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="a1832-151">La información de registro se almacena en una instancia de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a1832-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="a1832-152">La aplicación se compone de dos archivos (código para copiar y pegar disponible más abajo):</span><span class="sxs-lookup"><span data-stu-id="a1832-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="a1832-153">**index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.</span><span class="sxs-lookup"><span data-stu-id="a1832-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="a1832-154">**createtable.php**: crea la tabla de Base de datos SQL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1832-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="a1832-155">Este archivo solo se usará una vez.</span><span class="sxs-lookup"><span data-stu-id="a1832-155">This file will only be used once.</span></span>

<span data-ttu-id="a1832-156">Para ejecutar la aplicación localmente, realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="a1832-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="a1832-157">Tenga en cuenta que en estos pasos se supone que tiene PHP y SQL Server Express configurados en la máquina local, además de tener habilitada la [extensión PDO para SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="a1832-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="a1832-158">Cree una base de datos de SQL Server denominada `registration`.</span><span class="sxs-lookup"><span data-stu-id="a1832-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="a1832-159">Puede realizar este procedimiento desde el símbolo del sistema `sqlcmd` con estos comandos:</span><span class="sxs-lookup"><span data-stu-id="a1832-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="a1832-160">En el directorio raíz de la aplicación, cree dos archivos: uno llamado `createtable.php` y otro `index.php`.</span><span class="sxs-lookup"><span data-stu-id="a1832-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="a1832-161">Abra el archivo `createtable.php` en un editor de texto o IDE y agregue el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="a1832-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="a1832-162">Este código se usará para crear la tabla `registration_tbl` en la base de datos `registration`.</span><span class="sxs-lookup"><span data-stu-id="a1832-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="a1832-163">Tenga en cuenta que debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de SQL Server local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="a1832-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="a1832-164">En un terminal en el directorio raíz de la aplicación, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a1832-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="a1832-165">Abra un explorador web y vaya a **http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="a1832-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="a1832-166">Esto creará la tabla `registration_tbl` en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a1832-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="a1832-167">Abra el archivo **index.php** en un editor de texto o IDE y agregue el código HTML y CSS básico para la página (el código de PHP se agregará en pasos posteriores).</span><span class="sxs-lookup"><span data-stu-id="a1832-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="a1832-168">En las etiquetas de PHP, agregue el código de PHP para la conexión a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a1832-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="a1832-169">De nuevo, debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="a1832-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="a1832-170">Después del código de conexión a la base de datos, agregue el código para la inserción de información de registro en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a1832-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="a1832-171">Finalmente, después del código anterior, agregue el código para recuperar datos de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a1832-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="a1832-172">Ahora puede ir a **http://localhost:8000/index.php** para probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1832-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="a1832-173">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a1832-173">Publish your application</span></span>
<span data-ttu-id="a1832-174">Una vez que se haya probado la aplicación localmente, puede publicarla en Aplicaciones web del servicio de aplicaciones mediante Git.</span><span class="sxs-lookup"><span data-stu-id="a1832-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="a1832-175">Sin embargo, antes es necesario actualizar la información de la conexión a la base de datos en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1832-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="a1832-176">Con la información de conexión a la base de datos obtenida anteriormente (en la sección **Obtención de información de conexión de SQL**), actualice la siguiente información en **ambos** archivos `createdatabase.php` y `index.php` con los valores adecuados:</span><span class="sxs-lookup"><span data-stu-id="a1832-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="a1832-177">En el <code>$host</code>, el valor de servidor se debe anteponer con <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="a1832-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="a1832-178">Ahora, está listo para configurar la publicación de Git y publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1832-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="a1832-179">Estos son los mismos pasos que se indican al final de la sección **Creación de una aplicación web de Azure y configuración de la publicación Git** , más arriba.</span><span class="sxs-lookup"><span data-stu-id="a1832-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="a1832-180">Abra GitBash (o un terminal, si Git está en su `PATH`), cambie los directorios al directorio raíz de la aplicación (el directorio de **registro** )y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a1832-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="a1832-181">Se le solicitará la contraseña que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1832-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="a1832-182">Vaya a **http://[nombre de aplicación web].azurewebsites.net/createtable.php** para crear la tabla de Base de datos SQL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1832-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="a1832-183">Vaya a **http://[nombre de aplicación web].azurewebsites.net/index.php** para comenzar a usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1832-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="a1832-184">Una vez publicada la aplicación, podrá comenzar a realizar cambios en esta y a usar Git para publicarlos.</span><span class="sxs-lookup"><span data-stu-id="a1832-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="a1832-185">Publicación de cambios de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a1832-185">Publish changes to your application</span></span>
<span data-ttu-id="a1832-186">Para publicar los cambios de la aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a1832-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="a1832-187">Realice los cambios en la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="a1832-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="a1832-188">Abra GitBash (o un terminal, si Git está en su `PATH`), cambie los directorios al directorio raíz de la aplicación y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a1832-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="a1832-189">Se le solicitará la contraseña que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1832-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="a1832-190">Vaya a **http://[nombre de aplicación web].azurewebsites.net/index.php** para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="a1832-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a1832-191">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="a1832-191">What's changed</span></span>
* <span data-ttu-id="a1832-192">Para obtener una guía del cambio de Websites a App Service, consulte: [Azure App Service y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a1832-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

