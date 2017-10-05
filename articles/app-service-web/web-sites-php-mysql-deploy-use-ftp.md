---
title: "Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP"
description: "Tutorial en el que se muestra cómo crear una aplicación web PHP que almacena datos en MySQL y cómo usar la implementación de FTP en Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="f70f8-103">Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP</span><span class="sxs-lookup"><span data-stu-id="f70f8-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="f70f8-104">En este tutorial se muestra cómo crear una aplicación web PHP-MySQL y cómo implementarla mediante FTP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="f70f8-105">En este tutorial se supone que dispone de [PHP][install-php], [MySQL][install-mysql], un servidor web y un cliente FTP instalado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f70f8-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="f70f8-106">Las instrucciones de este tutorial se pueden seguir en cualquier sistema operativo, incluidos Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="f70f8-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="f70f8-107">Una vez completada esta guía, tendrá una aplicación web PHP/MySQL que se ejecutará en Azure.</span><span class="sxs-lookup"><span data-stu-id="f70f8-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="f70f8-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="f70f8-108">You will learn:</span></span>

* <span data-ttu-id="f70f8-109">Crear una aplicación web y una base de datos MySQL con el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f70f8-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="f70f8-110">Dado que PHP está habilitado en aplicaciones web de forma predeterminada, no existen requisitos especiales para ejecutar el código PHP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="f70f8-111">Publicar la aplicación en Azure mediante FTP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="f70f8-112">Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="f70f8-113">La aplicación se hospedará en una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f70f8-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="f70f8-114">A continuación se muestra una captura de pantalla de la aplicación completada:</span><span class="sxs-lookup"><span data-stu-id="f70f8-114">A screenshot of the completed application is below:</span></span>

![Sitio web PHP de Azure][running-app]

> [!NOTE]
> <span data-ttu-id="f70f8-116">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de registrarse para abrir una cuenta, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f70f8-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f70f8-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="f70f8-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="f70f8-118">Creación de una aplicación web y configuración de la publicación FTP</span><span class="sxs-lookup"><span data-stu-id="f70f8-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="f70f8-119">Siga estos pasos para crear una aplicación web y una base de datos MySQL:</span><span class="sxs-lookup"><span data-stu-id="f70f8-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="f70f8-120">Inicie sesión en [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="f70f8-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="f70f8-121">Haga clic en el icono **+Nuevo** de la parte superior izquierda del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f70f8-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Crear un sitio web de Azure][new-website]
3. <span data-ttu-id="f70f8-123">En la búsqueda, escriba **Aplicación web + MySQL** y haga clic en **Aplicación web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="f70f8-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Crear un sitio web personalizado][custom-create]
4. <span data-ttu-id="f70f8-125">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f70f8-125">Click **Create**.</span></span> <span data-ttu-id="f70f8-126">Escriba un nombre de servicio de aplicaciones único, un nombre válido para el grupo de recursos y un nuevo plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="f70f8-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Establecer nombre de grupo de recurso][resource-group]
5. <span data-ttu-id="f70f8-128">Especifique los valores para la nueva base de datos, incluida la aceptación de los términos legales.</span><span class="sxs-lookup"><span data-stu-id="f70f8-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Crear una base de datos MySQL][new-mysql-db]
6. <span data-ttu-id="f70f8-130">Una vez creada la aplicación web, verá la nueva hoja de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f70f8-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="f70f8-131">Haga clic en **Configuración** > **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="f70f8-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Configurar credenciales de implementación][set-deployment-credentials]
8. <span data-ttu-id="f70f8-133">Para habilitar la publicación FTP, debe proporcionar un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f70f8-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="f70f8-134">Guarde las credenciales y tome nota del nombre de usuario y la contraseña que cree.</span><span class="sxs-lookup"><span data-stu-id="f70f8-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Creación de credenciales de publicación][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="f70f8-136">Compilación y prueba local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f70f8-136">Build and test your app locally</span></span>
<span data-ttu-id="f70f8-137">Registration es una sencilla aplicación PHP que permite registrarse en un evento con solo proporcionar el nombre y la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="f70f8-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="f70f8-138">La información de los usuarios inscritos anteriormente se muestra en una tabla.</span><span class="sxs-lookup"><span data-stu-id="f70f8-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="f70f8-139">La información de registro se almacena en una base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="f70f8-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="f70f8-140">La aplicación consta de dos archivos:</span><span class="sxs-lookup"><span data-stu-id="f70f8-140">The app consists of two files:</span></span>

* <span data-ttu-id="f70f8-141">**index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.</span><span class="sxs-lookup"><span data-stu-id="f70f8-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="f70f8-142">**createtable.php**: crea la tabla MySQL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f70f8-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="f70f8-143">Este archivo solo se usará una vez.</span><span class="sxs-lookup"><span data-stu-id="f70f8-143">This file will only be used once.</span></span>

<span data-ttu-id="f70f8-144">Para compilar y ejecutar la aplicación localmente, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="f70f8-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="f70f8-145">Tenga en cuenta que en estos pasos se presupone que tiene PHP, MySQL y un servidor web configurado en la máquina local, además de tener habilitada la [extensión PDO para MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="f70f8-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="f70f8-146">Cree una base de datos MySQL llamada `registration`.</span><span class="sxs-lookup"><span data-stu-id="f70f8-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="f70f8-147">Puede realizar este procedimiento desde el símbolo del sistema de MySQL con este comando:</span><span class="sxs-lookup"><span data-stu-id="f70f8-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="f70f8-148">En el directorio raíz del servidor web, cree una carpeta llamada `registration` y dos archivos en ella: uno llamado `createtable.php` y otro `index.php`.</span><span class="sxs-lookup"><span data-stu-id="f70f8-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="f70f8-149">Abra el archivo `createtable.php` en un editor de texto o IDE y agregue el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="f70f8-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="f70f8-150">Este código se usará para crear la tabla `registration_tbl` en la base de datos `registration`.</span><span class="sxs-lookup"><span data-stu-id="f70f8-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="f70f8-151">Debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f70f8-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="f70f8-152">Abra un explorador web y vaya a [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="f70f8-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="f70f8-153">Esto creará la tabla `registration_tbl` en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f70f8-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="f70f8-154">Abra el archivo **index.php** en un editor de texto o IDE y agregue el código HTML y CSS básico para la página (el código de PHP se agregará en pasos posteriores).</span><span class="sxs-lookup"><span data-stu-id="f70f8-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="f70f8-155">En las etiquetas de PHP, agregue el código de PHP para la conexión a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f70f8-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="f70f8-156">De nuevo, debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f70f8-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="f70f8-157">Después del código de conexión a la base de datos, agregue el código para la inserción de información de registro en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f70f8-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="f70f8-158">Finalmente, después del código anterior, agregue el código para recuperar datos de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f70f8-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="f70f8-159">Ahora puede dirigirse a [http://localhost/registration/index.php][localhost-index] para probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f70f8-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="f70f8-160">Obtención de información de conexión de FTP y MySQL</span><span class="sxs-lookup"><span data-stu-id="f70f8-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="f70f8-161">Para conectarse a la base de datos MySQL que se ejecuta en aplicaciones web, necesita información de conexión.</span><span class="sxs-lookup"><span data-stu-id="f70f8-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="f70f8-162">Si desea obtener la información de conexión de MySQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f70f8-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="f70f8-163">En la hoja de la aplicación web del servicio de aplicaciones, haga clic en el vínculo del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="f70f8-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Selección de grupo de recursos][select-resourcegroup]
2. <span data-ttu-id="f70f8-165">En el grupo de recursos, haga clic en la base de datos:</span><span class="sxs-lookup"><span data-stu-id="f70f8-165">From your resource group, click the database:</span></span>
   
    ![Seleccionar base de datos][select-database]
3. <span data-ttu-id="f70f8-167">En el resumen de base de datos, seleccione **Configuración** > **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="f70f8-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Seleccionar propiedades][select-properties]
4. <span data-ttu-id="f70f8-169">Anote los valores de `Database`, `Host`, `User Id` y `Password`.</span><span class="sxs-lookup"><span data-stu-id="f70f8-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Anotar propiedades][note-properties]
5. <span data-ttu-id="f70f8-171">En la aplicación web, haga clic en el vínculo **Descargar perfil de publicación** situado en la esquina inferior derecha de la página:</span><span class="sxs-lookup"><span data-stu-id="f70f8-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Descargar perfil de publicación][download-publish-profile]
6. <span data-ttu-id="f70f8-173">Abra el archivo `.publishsettings` en un editor XML.</span><span class="sxs-lookup"><span data-stu-id="f70f8-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="f70f8-174">Busque el elemento `<publishProfile >` con `publishMethod="FTP"` que se parece a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f70f8-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="f70f8-175">Tome nota de los atributos `publishUrl`, `userName` y `userPWD` .</span><span class="sxs-lookup"><span data-stu-id="f70f8-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="f70f8-176">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f70f8-176">Publish your app</span></span>
<span data-ttu-id="f70f8-177">Una vez que se haya probado la aplicación localmente, esta puede publicarse en la aplicación web mediante FTP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="f70f8-178">Sin embargo, antes es necesario actualizar la información de la conexión a la base de datos en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f70f8-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="f70f8-179">Con la información de conexión a la base de datos obtenida anteriormente (en la sección **Obtención de información de conexión de FTP y MySQL**), actualice la siguiente información en **ambos** archivos `createdatabase.php` y `index.php` con los valores adecuados:</span><span class="sxs-lookup"><span data-stu-id="f70f8-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="f70f8-180">Ahora está listo para publicar la aplicación mediante FTP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="f70f8-181">Abra el cliente FTP que desee.</span><span class="sxs-lookup"><span data-stu-id="f70f8-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="f70f8-182">Especifique la *parte del nombre de host* del atributo `publishUrl` que anotó anteriormente en el cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="f70f8-183">Escriba sin modificar los atributos `userName` y `userPWD` que anotó anteriormente en el cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="f70f8-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="f70f8-184">Establezca una conexión.</span><span class="sxs-lookup"><span data-stu-id="f70f8-184">Establish a connection.</span></span>

<span data-ttu-id="f70f8-185">Una vez que haya conseguido conectarse, podrá cargar y descargar archivos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f70f8-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="f70f8-186">Asegúrese de que está cargando los archivos en el directorio raíz, que es `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="f70f8-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="f70f8-187">Después de cargar `index.php` y `createtable.php`, vaya a **http://[nombre de sitio].azurewebsites.net/createtable.php** para crear una tabla MySQL para la aplicación y, a continuación, vaya a **http://[nombre sitio].azurewebsites.net/index.php** para comenzar a usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f70f8-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f70f8-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f70f8-188">Next steps</span></span>
<span data-ttu-id="f70f8-189">Para obtener más información, consulte el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f70f8-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

