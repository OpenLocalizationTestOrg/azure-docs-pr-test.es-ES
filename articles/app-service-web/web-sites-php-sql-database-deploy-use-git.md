---
title: "aaaCreate PHP T-SQL aplicación web e implementar tooAzure servicio de aplicaciones mediante Git"
description: "Un tutorial que muestra la aplicación que almacena los datos en la base de datos de SQL Azure web toocreate un PHP y el uso de Git implementación tooAzure servicio de aplicaciones."
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
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="852ef-103">Crear una aplicación web de PHP SQL e implementar tooAzure servicio de aplicaciones mediante Git</span><span class="sxs-lookup"><span data-stu-id="852ef-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="852ef-104">Este tutorial muestra cómo toocreate un PHP web app en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que conecta tooAzure base de datos SQL y cómo toodeploy con Git.</span><span class="sxs-lookup"><span data-stu-id="852ef-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="852ef-105">Este tutorial se da por supuesto que tiene [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers para SQL Server para PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), y [Git] [ install-git] instalados en su equipo.</span><span class="sxs-lookup"><span data-stu-id="852ef-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="852ef-106">Una vez completada esta guía, tendrá una aplicación web PHP-SQL que se ejecutará en Azure.</span><span class="sxs-lookup"><span data-stu-id="852ef-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="852ef-107">Puede instalar y configurar Microsoft Drivers de hello, SQL Server Express y PHP para SQL Server para PHP con hello [instalador de plataforma Web de Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="852ef-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="852ef-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="852ef-108">You will learn:</span></span>

* <span data-ttu-id="852ef-109">Cómo toocreate una Azure web app y una base de datos SQL hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="852ef-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="852ef-110">Como PHP está habilitado en la aplicación del servicio de aplicaciones Web de forma predeterminada, nada especial es toorun requiere el código PHP.</span><span class="sxs-lookup"><span data-stu-id="852ef-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="852ef-111">¿Cómo toopublish y volver a publicar el tooAzure de aplicación mediante Git.</span><span class="sxs-lookup"><span data-stu-id="852ef-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="852ef-112">Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP</span><span class="sxs-lookup"><span data-stu-id="852ef-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="852ef-113">aplicación Hello se hospedará en un sitio Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="852ef-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="852ef-114">Una captura de pantalla de la aplicación hello completado es menor que:</span><span class="sxs-lookup"><span data-stu-id="852ef-114">A screenshot of hello completed application is below:</span></span>

![Sitio web PHP de Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="852ef-116">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="852ef-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="852ef-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="852ef-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="852ef-118">Creación de una aplicación web de Azure y configuración de la publicación Git</span><span class="sxs-lookup"><span data-stu-id="852ef-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="852ef-119">Siga estos toocreate pasos una aplicación web de Azure y una base de datos de SQL:</span><span class="sxs-lookup"><span data-stu-id="852ef-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="852ef-120">Inicie sesión en toohello [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="852ef-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="852ef-121">Abra hello Azure Marketplace, haga clic en hello **New** icono situado en la parte superior de hello izquierda del panel de hello, haga clic en **seleccionar todo** tooMarketplace y seleccione siguiente **Web y móvil**.</span><span class="sxs-lookup"><span data-stu-id="852ef-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="852ef-122">Hola Marketplace, seleccione **Web y móvil**.</span><span class="sxs-lookup"><span data-stu-id="852ef-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="852ef-123">Haga clic en hello **Web app + SQL** icono.</span><span class="sxs-lookup"><span data-stu-id="852ef-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="852ef-124">Después de leer la descripción de Hola de aplicación de hello Web + SQL aplicación, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="852ef-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="852ef-125">Haga clic en cada parte (**grupo de recursos**, **aplicación Web**, **base de datos**, y **suscripción**) y escriba o seleccione valores de hello necesarios campos:</span><span class="sxs-lookup"><span data-stu-id="852ef-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="852ef-126">Escriba un nombre de URL de su elección.</span><span class="sxs-lookup"><span data-stu-id="852ef-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="852ef-127">Configuración de credenciales de servidor de bases de datos</span><span class="sxs-lookup"><span data-stu-id="852ef-127">Configure database server credentials</span></span>
   * <span data-ttu-id="852ef-128">Seleccione Hola región más cercana tooyou</span><span class="sxs-lookup"><span data-stu-id="852ef-128">Select hello region closest tooyou</span></span>
     
     ![configurar su aplicación](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="852ef-130">Cuando termine la definición de aplicación web de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="852ef-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="852ef-131">Cuando se ha creado la aplicación web de hello, Hola **notificaciones** botón parpadeará en un color verde **correcto** y Hola tooshow abierto de hoja de grupo de recursos de ambos hello web hello y aplicación de base de datos SQL en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ef-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="852ef-132">Haga clic en el icono de la aplicación hello web en la hoja de hello recursos grupo hoja tooopen Hola aplicación web.</span><span class="sxs-lookup"><span data-stu-id="852ef-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![Grupo de recursos de la aplicación web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="852ef-134">En **Configuración**, haga clic en **Implementación continua** > **Configurar los valores obligatorios**.</span><span class="sxs-lookup"><span data-stu-id="852ef-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="852ef-135">Seleccione **Repositorio de Git local** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="852ef-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![Dónde está su código fuente](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="852ef-137">Si no ha configurado antes un repositorio de Git, debe facilitar un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="852ef-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="852ef-138">toodo, haga clic en **configuración** > **las credenciales de implementación** de hoja de la aplicación hello web.</span><span class="sxs-lookup"><span data-stu-id="852ef-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="852ef-139">En **configuración** haga clic en **propiedades** toosee Hola Git dirección URL remota que necesite toouse toodeploy la aplicación PHP más adelante.</span><span class="sxs-lookup"><span data-stu-id="852ef-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="852ef-140">Obtención de información de conexión de la Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="852ef-140">Get SQL Database connection information</span></span>
<span data-ttu-id="852ef-141">instancia de base de datos SQL de toohello tooconnect que está vinculada tooyour web app, su voluntad necesita Hola información de conexión, que especificó cuando creó la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ef-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="852ef-142">Hola tooget información de conexión de base de datos SQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="852ef-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="852ef-143">En la hoja del grupo de recursos de hello, haga clic en el icono de hello SQL la base de datos.</span><span class="sxs-lookup"><span data-stu-id="852ef-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="852ef-144">En la hoja de hello SQL la base de datos, haga clic en **configuración** > **propiedades**, a continuación, haga clic en **mostrar cadenas de conexión de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="852ef-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Ver las propiedades de una base de datos](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="852ef-146">De hello **PHP** sección del cuadro de diálogo resultante de hello, tome nota de los valores de hello para `Server`, `SQL Database`, y `User Name`.</span><span class="sxs-lookup"><span data-stu-id="852ef-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="852ef-147">Usará estos valores más adelante al publicar su aplicación de web PHP tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="852ef-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="852ef-148">Compilación y comprobación de la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="852ef-148">Build and test your application locally</span></span>
<span data-ttu-id="852ef-149">aplicación de registro de Hello es una sencilla aplicación de PHP que permite tooregister para un evento proporcionando su nombre y direcciones de correo.</span><span class="sxs-lookup"><span data-stu-id="852ef-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="852ef-150">La información de los usuarios inscritos anteriormente se muestra en una tabla.</span><span class="sxs-lookup"><span data-stu-id="852ef-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="852ef-151">La información de registro se almacena en una instancia de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="852ef-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="852ef-152">aplicación Hello consta de dos archivos (copiar y pegar código disponible a continuación):</span><span class="sxs-lookup"><span data-stu-id="852ef-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="852ef-153">**index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.</span><span class="sxs-lookup"><span data-stu-id="852ef-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="852ef-154">**CreateTable.PHP**: crea la tabla de base de datos SQL de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="852ef-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="852ef-155">Este archivo solo se usará una vez.</span><span class="sxs-lookup"><span data-stu-id="852ef-155">This file will only be used once.</span></span>

<span data-ttu-id="852ef-156">aplicación de hello toorun localmente, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="852ef-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="852ef-157">Tenga en cuenta que estos pasos se supone tener PHP y SQL Server Express configurado en el equipo local y que se ha habilitado Hola [extensión PDO para SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="852ef-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="852ef-158">Cree una base de datos de SQL Server denominada `registration`.</span><span class="sxs-lookup"><span data-stu-id="852ef-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="852ef-159">Puede hacerlo desde hello `sqlcmd` símbolo del sistema con estos comandos:</span><span class="sxs-lookup"><span data-stu-id="852ef-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="852ef-160">En el directorio raíz de la aplicación, cree dos archivos: uno llamado `createtable.php` y otro `index.php`.</span><span class="sxs-lookup"><span data-stu-id="852ef-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="852ef-161">Abra hello `createtable.php` un archivo en un editor de texto o IDE y agregar código de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="852ef-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="852ef-162">Este código será usado toocreate hello `registration_tbl` tabla Hola `registration` base de datos.</span><span class="sxs-lookup"><span data-stu-id="852ef-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   
    <span data-ttu-id="852ef-163">Tenga en cuenta que necesitará valores de hello tooupdate para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de SQL Server local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="852ef-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="852ef-164">En un terminal en directorio de raíz de Hola de Hola Hola de tipo de aplicación siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="852ef-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="852ef-165">Abra un explorador web y vaya demasiado**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="852ef-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="852ef-166">Esto creará hello `registration_tbl` tabla de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ef-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="852ef-167">Abra hello **index.php** un archivo en un editor de texto o IDE y agregue los código básico de HTML y CSS de hello para la página de hello (Hola código PHP se agregará en pasos posteriores).</span><span class="sxs-lookup"><span data-stu-id="852ef-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="852ef-168">Dentro de las etiquetas PHP hello, agregue el código PHP para la conexión de base de datos de toohello.</span><span class="sxs-lookup"><span data-stu-id="852ef-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="852ef-169">De nuevo, se necesita valores de hello tooupdate para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="852ef-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="852ef-170">Código de conexión de base de datos de hello, siguiente, agregue código para insertar información de registro en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ef-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
9. <span data-ttu-id="852ef-171">Finalmente, después de hello código anterior, agregue código para recuperar datos de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="852ef-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="852ef-172">Ahora puede examinar demasiado**http://localhost:8000/index.php** aplicación de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="852ef-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="852ef-173">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="852ef-173">Publish your application</span></span>
<span data-ttu-id="852ef-174">Después de haber probado la aplicación localmente, se pueden publicar aplicaciones Web del servicio tooApp usando Git.</span><span class="sxs-lookup"><span data-stu-id="852ef-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="852ef-175">Sin embargo, primero necesita información de conexión de base de datos de tooupdate hello en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="852ef-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="852ef-176">Usando la información de conexión de base de datos de hello obtenido anteriormente (en hello **información de conexión de base de datos de SQL obtener** sección), Hola de actualización siguiente información en **ambos** hello `createdatabase.php` y `index.php` archivos con hello los valores adecuados:</span><span class="sxs-lookup"><span data-stu-id="852ef-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="852ef-177">Hola <code>$host</code>, valor de saludo del servidor se debe anteponer con <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="852ef-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="852ef-178">Ahora, está listo tooset la publicación de Git y publicar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="852ef-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="852ef-179">Se trata de hello mismos pasos se indican al final de Hola de hello **crear una aplicación web de Azure y configurar la publicación de Git** sección anterior.</span><span class="sxs-lookup"><span data-stu-id="852ef-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="852ef-180">Abrir GitBash (o un terminal, si está Git en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación (hello **registro** directorio), y ejecución Hola siguiendo comandos:</span><span class="sxs-lookup"><span data-stu-id="852ef-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="852ef-181">Se le pedirá para contraseña de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="852ef-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="852ef-182">Examinar demasiado**http://[web aplicación name].azurewebsites.net/createtable.php** tabla de base de datos SQL toocreate hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="852ef-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="852ef-183">Examinar demasiado**http://[web aplicación name].azurewebsites.net/index.php** toobegin mediante la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="852ef-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="852ef-184">Después de publicar la aplicación, puede empezar a realizar cambios tooit y usar Git toopublish ellos.</span><span class="sxs-lookup"><span data-stu-id="852ef-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="852ef-185">Publicar aplicación de tooyour de cambios</span><span class="sxs-lookup"><span data-stu-id="852ef-185">Publish changes tooyour application</span></span>
<span data-ttu-id="852ef-186">toopublish cambia tooapplication, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="852ef-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="852ef-187">Realizar cambios tooyour aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="852ef-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="852ef-188">Abra GitBash (o un terminal, TI Git está en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación y ejecutar Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="852ef-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="852ef-189">Se le pedirá para contraseña de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="852ef-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="852ef-190">Examinar demasiado**http://[web aplicación name].azurewebsites.net/index.php** toosee los cambios.</span><span class="sxs-lookup"><span data-stu-id="852ef-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="852ef-191">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="852ef-191">What's changed</span></span>
* <span data-ttu-id="852ef-192">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="852ef-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

