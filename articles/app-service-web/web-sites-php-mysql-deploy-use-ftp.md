---
title: "aaaCreate un MySQL PHP web de aplicación de servicio de aplicaciones de Azure e implementar mediante FTP"
description: "Un tutorial que demuestra cómo toocreate un PHP web app que almacena los datos de uso y MySQL tooAzure de implementación FTP."
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
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="f6776-103">Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP</span><span class="sxs-lookup"><span data-stu-id="f6776-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="f6776-104">Este tutorial muestra cómo toocreate un MySQL PHP de aplicación web y cómo toodeploy a través de FTP.</span><span class="sxs-lookup"><span data-stu-id="f6776-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="f6776-105">En este tutorial se supone que dispone de [PHP][install-php], [MySQL][install-mysql], un servidor web y un cliente FTP instalado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f6776-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="f6776-106">instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo, incluidos Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="f6776-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="f6776-107">Una vez completada esta guía, tendrá una aplicación web PHP/MySQL que se ejecutará en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6776-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="f6776-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="f6776-108">You will learn:</span></span>

* <span data-ttu-id="f6776-109">Cómo toocreate una aplicación web y un MySQL base de datos utilizando Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6776-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="f6776-110">Como PHP está habilitado en las aplicaciones Web de forma predeterminada, nada especial es toorun requiere el código PHP.</span><span class="sxs-lookup"><span data-stu-id="f6776-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="f6776-111">Cómo toopublish tooAzure aplicación mediante FTP.</span><span class="sxs-lookup"><span data-stu-id="f6776-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="f6776-112">Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP.</span><span class="sxs-lookup"><span data-stu-id="f6776-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="f6776-113">aplicación Hello se hospeda en una aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="f6776-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="f6776-114">Una captura de pantalla de la aplicación hello completado es menor que:</span><span class="sxs-lookup"><span data-stu-id="f6776-114">A screenshot of hello completed application is below:</span></span>

![Sitio web PHP de Azure][running-app]

> [!NOTE]
> <span data-ttu-id="f6776-116">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f6776-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f6776-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="f6776-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="f6776-118">Creación de una aplicación web y configuración de la publicación FTP</span><span class="sxs-lookup"><span data-stu-id="f6776-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="f6776-119">Siga estos pasos toocreate una aplicación web y una base de datos de MySQL:</span><span class="sxs-lookup"><span data-stu-id="f6776-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="f6776-120">Inicio de sesión toohello [Portal de Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="f6776-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="f6776-121">Haga clic en hello **+ nuevo** icono situado en la parte superior de hello izquierda de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6776-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Crear un sitio web de Azure][new-website]
3. <span data-ttu-id="f6776-123">En el tipo de búsqueda de hello **Web app + MySQL** y haga clic en **Web app + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="f6776-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Crear un sitio web personalizado][custom-create]
4. <span data-ttu-id="f6776-125">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f6776-125">Click **Create**.</span></span> <span data-ttu-id="f6776-126">Escriba un nombre de servicio de aplicaciones único, un nombre válido para el grupo de recursos de Hola y un nuevo plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="f6776-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![Establecer nombre de grupo de recurso][resource-group]
5. <span data-ttu-id="f6776-128">Especifique valores para la nueva base de datos, incluidos los acepta los términos legales toohello.</span><span class="sxs-lookup"><span data-stu-id="f6776-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Crear una base de datos MySQL][new-mysql-db]
6. <span data-ttu-id="f6776-130">Cuando se ha creado la aplicación web de hello, verá la nueva hoja de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="f6776-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="f6776-131">Haga clic en **Configuración** > **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="f6776-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Configurar credenciales de implementación][set-deployment-credentials]
8. <span data-ttu-id="f6776-133">tooenable publicación FTP, debe proporcionar un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f6776-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="f6776-134">Guardar las credenciales de Hola y tome nota del nombre de usuario de Hola y la contraseña que se crea.</span><span class="sxs-lookup"><span data-stu-id="f6776-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![Creación de credenciales de publicación][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="f6776-136">Compilación y prueba local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f6776-136">Build and test your app locally</span></span>
<span data-ttu-id="f6776-137">aplicación de registro de Hello es una sencilla aplicación de PHP que permite tooregister para un evento proporcionando su nombre y direcciones de correo.</span><span class="sxs-lookup"><span data-stu-id="f6776-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="f6776-138">La información de los usuarios inscritos anteriormente se muestra en una tabla.</span><span class="sxs-lookup"><span data-stu-id="f6776-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="f6776-139">La información de registro se almacena en una base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="f6776-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="f6776-140">aplicación Hello consta de dos archivos:</span><span class="sxs-lookup"><span data-stu-id="f6776-140">hello app consists of two files:</span></span>

* <span data-ttu-id="f6776-141">**index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.</span><span class="sxs-lookup"><span data-stu-id="f6776-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="f6776-142">**CreateTable.PHP**: crea la tabla de MySQL de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6776-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="f6776-143">Este archivo solo se usará una vez.</span><span class="sxs-lookup"><span data-stu-id="f6776-143">This file will only be used once.</span></span>

<span data-ttu-id="f6776-144">toobuild y aplicación de hello ejecución localmente, siga los pasos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="f6776-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="f6776-145">Tenga en cuenta que estos pasos se supone que tiene PHP, MySQL y un servidor web configurado en el equipo local y que se ha habilitado Hola [extensión PDO para MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="f6776-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="f6776-146">Cree una base de datos MySQL llamada `registration`.</span><span class="sxs-lookup"><span data-stu-id="f6776-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="f6776-147">Puede hacerlo desde la línea de comandos de MySQL Hola con este comando:</span><span class="sxs-lookup"><span data-stu-id="f6776-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="f6776-148">En el directorio raíz del servidor web, cree una carpeta llamada `registration` y dos archivos en ella: uno llamado `createtable.php` y otro `index.php`.</span><span class="sxs-lookup"><span data-stu-id="f6776-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="f6776-149">Abra hello `createtable.php` un archivo en un editor de texto o IDE y agregar código de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="f6776-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="f6776-150">Este código será usado toocreate hello `registration_tbl` tabla Hola `registration` base de datos.</span><span class="sxs-lookup"><span data-stu-id="f6776-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   > <span data-ttu-id="f6776-151">Necesitará tooupdate Hola valores para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f6776-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="f6776-152">Abra un explorador web y vaya demasiado[http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="f6776-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="f6776-153">Esto creará hello `registration_tbl` tabla de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6776-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="f6776-154">Abra hello **index.php** un archivo en un editor de texto o IDE y agregue los código básico de HTML y CSS de hello para la página de hello (Hola código PHP se agregará en pasos posteriores).</span><span class="sxs-lookup"><span data-stu-id="f6776-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="f6776-155">Dentro de las etiquetas PHP hello, agregue el código PHP para la conexión de base de datos de toohello.</span><span class="sxs-lookup"><span data-stu-id="f6776-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="f6776-156">De nuevo, se necesita valores de hello tooupdate para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f6776-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="f6776-157">Código de conexión de base de datos de hello, siguiente, agregue código para insertar información de registro en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6776-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="f6776-158">Finalmente, después de hello código anterior, agregue código para recuperar datos de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6776-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="f6776-159">Ahora puede examinar demasiado[http://localhost/registration/index.php] [ localhost-index] tootest Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6776-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="f6776-160">Obtención de información de conexión de FTP y MySQL</span><span class="sxs-lookup"><span data-stu-id="f6776-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="f6776-161">tooconnect toohello MySQL base de datos se ejecuta en las aplicaciones Web, su voluntad necesita Hola información de conexión.</span><span class="sxs-lookup"><span data-stu-id="f6776-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="f6776-162">tooget información de conexión de MySQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f6776-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="f6776-163">De servicio de aplicaciones de hello hoja de la aplicación web, haga clic en el vínculo de grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="f6776-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![Selección de grupo de recursos][select-resourcegroup]
2. <span data-ttu-id="f6776-165">En el grupo de recursos, haga clic en base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="f6776-165">From your resource group, click hello database:</span></span>
   
    ![Seleccionar base de datos][select-database]
3. <span data-ttu-id="f6776-167">En la base de datos de hello resumen, seleccione **configuración** > **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="f6776-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![Seleccionar propiedades][select-properties]
4. <span data-ttu-id="f6776-169">Tome nota de los valores de hello para `Database`, `Host`, `User Id`, y `Password`.</span><span class="sxs-lookup"><span data-stu-id="f6776-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Anotar propiedades][note-properties]
5. <span data-ttu-id="f6776-171">Desde la aplicación web, haga clic en hello **descargar perfil de publicación** en hello esquina inferior derecha de la página de hello vínculo:</span><span class="sxs-lookup"><span data-stu-id="f6776-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Descargar perfil de publicación][download-publish-profile]
6. <span data-ttu-id="f6776-173">Abra hello `.publishsettings` archivo en un editor XML.</span><span class="sxs-lookup"><span data-stu-id="f6776-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="f6776-174">Buscar hello `<publishProfile >` elemento con `publishMethod="FTP"` que busca toothis similar:</span><span class="sxs-lookup"><span data-stu-id="f6776-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="f6776-175">Tome nota de hello `publishUrl`, `userName`, y `userPWD` atributos.</span><span class="sxs-lookup"><span data-stu-id="f6776-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="f6776-176">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f6776-176">Publish your app</span></span>
<span data-ttu-id="f6776-177">Después de haber probado la aplicación localmente, puede publicarlo tooyour web app mediante FTP.</span><span class="sxs-lookup"><span data-stu-id="f6776-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="f6776-178">Sin embargo, primero necesita información de conexión de base de datos de tooupdate hello en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6776-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="f6776-179">Usando la información de conexión de base de datos de hello obtenido anteriormente (en hello **información de conexión FTP y obtener MySQL** sección), Hola de actualización siguiente información en **ambos** hello `createdatabase.php` y `index.php` archivos con hello los valores adecuados:</span><span class="sxs-lookup"><span data-stu-id="f6776-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="f6776-180">Ahora está listo toopublish su aplicación mediante FTP.</span><span class="sxs-lookup"><span data-stu-id="f6776-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="f6776-181">Abra el cliente FTP que desee.</span><span class="sxs-lookup"><span data-stu-id="f6776-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="f6776-182">Escriba hello *parte del nombre de host* de hello `publishUrl` atributo indicados anteriormente en el cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="f6776-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="f6776-183">Escriba hello `userName` y `userPWD` sin modificar atributos mencionados anteriormente en el cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="f6776-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="f6776-184">Establezca una conexión.</span><span class="sxs-lookup"><span data-stu-id="f6776-184">Establish a connection.</span></span>

<span data-ttu-id="f6776-185">Después de haberse conectado se ser capaz de tooupload y descargar archivos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f6776-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="f6776-186">Asegúrese de que esté cargando el directorio raíz de toohello de archivos, que es `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="f6776-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="f6776-187">Después de cargar ambos `index.php` y `createtable.php`, examinar demasiado**http://[site name].azurewebsites.net/createtable.php** toocreate Hola MySQL de la tabla de la aplicación hello, a continuación, examinar demasiado**http://[site nombre ].azurewebsites.net/index.php** toobegin mediante la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6776-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6776-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6776-188">Next steps</span></span>
<span data-ttu-id="f6776-189">Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f6776-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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

