---
title: "Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante Git"
description: "Tutorial en el que se muestra cómo crear una aplicación web PHP que almacena datos en MySQL y usar la implementación de Git en Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="69df8-103">Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante Git</span><span class="sxs-lookup"><span data-stu-id="69df8-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="69df8-104">En este tutorial se muestra cómo crear una aplicación web PHP-MySQL y cómo implementarla en el [Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) mediante Git.</span><span class="sxs-lookup"><span data-stu-id="69df8-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="69df8-105">Usará [PHP][install-php], la herramienta de línea de comandos MySQL (parte de [MySQL][install-mysql]) y [Git][install-git] instalados en el equipo.</span><span class="sxs-lookup"><span data-stu-id="69df8-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="69df8-106">Las instrucciones de este tutorial se pueden seguir en cualquier sistema operativo, incluidos Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="69df8-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="69df8-107">Una vez completada esta guía, tendrá una aplicación web PHP/MySQL que se ejecutará en Azure.</span><span class="sxs-lookup"><span data-stu-id="69df8-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="69df8-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="69df8-108">You will learn:</span></span>

* <span data-ttu-id="69df8-109">Crear una aplicación web y una base de datos MySQL con [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="69df8-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="69df8-110">Dado que PHP está habilitado en [Aplicaciones web del Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) de forma predeterminada, no existen requisitos especiales para ejecutar el código PHP.</span><span class="sxs-lookup"><span data-stu-id="69df8-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="69df8-111">Publicar y volver a publicar la aplicación en Azure con Git.</span><span class="sxs-lookup"><span data-stu-id="69df8-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="69df8-112">Habilitar la extensión de Composer para automatizar las tareas de Composer en cada `git push`.</span><span class="sxs-lookup"><span data-stu-id="69df8-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="69df8-113">Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP.</span><span class="sxs-lookup"><span data-stu-id="69df8-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="69df8-114">La aplicación se hospedará en aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="69df8-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="69df8-115">A continuación se muestra una captura de pantalla de la aplicación completada:</span><span class="sxs-lookup"><span data-stu-id="69df8-115">A screenshot of the completed application is below:</span></span>

![Sitio web PHP de Azure][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="69df8-117">Configuración del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="69df8-117">Set up the development environment</span></span>
<span data-ttu-id="69df8-118">En este tutorial se supone que tiene [PHP][install-php], la herramienta de línea de comandos MySQL (parte de [MySQL][install-mysql]) y [Git][install-git] instalados en el equipo.</span><span class="sxs-lookup"><span data-stu-id="69df8-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="69df8-119">Creación de una aplicación web y configuración de la publicación Git</span><span class="sxs-lookup"><span data-stu-id="69df8-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="69df8-120">Siga estos pasos para crear una aplicación web y una base de datos MySQL:</span><span class="sxs-lookup"><span data-stu-id="69df8-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="69df8-121">Inicie sesión en [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="69df8-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="69df8-122">Haga clic en el icono **Nuevo** .</span><span class="sxs-lookup"><span data-stu-id="69df8-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="69df8-123">Haga clic en **Ver todo** junto a **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="69df8-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="69df8-124">Haga clic en **Web + móvil** y, a continuación, en **Aplicación web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="69df8-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="69df8-125">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="69df8-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="69df8-126">Escriba un nombre válido para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="69df8-126">Enter a valid name for your resource group.</span></span>
   
    ![Establecer nombre de grupo de recurso][resource-group]
6. <span data-ttu-id="69df8-128">Escriba valores para la nueva aplicación web.</span><span class="sxs-lookup"><span data-stu-id="69df8-128">Enter values for your new web app.</span></span>
   
    ![Crear una aplicación web][new-web-app]
7. <span data-ttu-id="69df8-130">Especifique los valores para la nueva base de datos, incluida la aceptación de los términos legales.</span><span class="sxs-lookup"><span data-stu-id="69df8-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Crear una base de datos MySQL][new-mysql-db]
8. <span data-ttu-id="69df8-132">Una vez creada la aplicación web, verá la nueva hoja de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="69df8-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="69df8-133">En **Configuración**, haga clic en **Implementación continua** y, a continuación, en *Configurar los valores obligatorios*.</span><span class="sxs-lookup"><span data-stu-id="69df8-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configuración de la publicación Git][setup-publishing]
10. <span data-ttu-id="69df8-135">Seleccione **Repositorio de Git local** para el origen.</span><span class="sxs-lookup"><span data-stu-id="69df8-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Configuración de un repositorio Git][setup-repository]
11. <span data-ttu-id="69df8-137">Para habilitar la publicación Git, debe proporcionar un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="69df8-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="69df8-138">Tome nota de ambos.</span><span class="sxs-lookup"><span data-stu-id="69df8-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="69df8-139">(Si ya ha configurado un repositorio Git anteriormente, este paso se omitirá).</span><span class="sxs-lookup"><span data-stu-id="69df8-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Creación de credenciales de publicación][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="69df8-141">Obtención de información de la conexión MySQL remota</span><span class="sxs-lookup"><span data-stu-id="69df8-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="69df8-142">Para conectarse a la base de datos MySQL que se ejecuta en aplicaciones web, necesita información de conexión.</span><span class="sxs-lookup"><span data-stu-id="69df8-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="69df8-143">Si desea obtener la información de conexión de MySQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="69df8-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="69df8-144">En el grupo de recursos, haga clic en la base de datos:</span><span class="sxs-lookup"><span data-stu-id="69df8-144">From your resource group, click the database:</span></span>
   
    ![Seleccionar base de datos][select-database]
2. <span data-ttu-id="69df8-146">En la **Configuración** de la base de datos, seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="69df8-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![Seleccionar propiedades][select-properties]
3. <span data-ttu-id="69df8-148">Anote los valores de `Database`, `Host`, `User Id` y `Password`.</span><span class="sxs-lookup"><span data-stu-id="69df8-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Anotar propiedades][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="69df8-150">Compilación y prueba local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="69df8-150">Build and test your app locally</span></span>
<span data-ttu-id="69df8-151">Ahora que ha creado una aplicación web, puede desarrollarla localmente e implementarla después de las pruebas.</span><span class="sxs-lookup"><span data-stu-id="69df8-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="69df8-152">Registration es una sencilla aplicación PHP que permite registrarse en un evento con solo proporcionar el nombre y la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="69df8-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="69df8-153">La información de los usuarios inscritos anteriormente se muestra en una tabla.</span><span class="sxs-lookup"><span data-stu-id="69df8-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="69df8-154">La información de registro se almacena en una base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="69df8-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="69df8-155">La aplicación se compone de un archivo (código para copiar y pegar disponible más abajo).</span><span class="sxs-lookup"><span data-stu-id="69df8-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="69df8-156">**index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.</span><span class="sxs-lookup"><span data-stu-id="69df8-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="69df8-157">Para compilar y ejecutar la aplicación localmente, realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="69df8-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="69df8-158">Tenga en cuenta que en estos pasos se supone que tiene PHP y la herramienta de línea de comandos MySQL (parte de MySQL) configurados en la máquina local, además de tener habilitada la [extensión PDO para MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="69df8-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="69df8-159">Conéctese al servidor MySQL remoto usando los valores de `Data Source`, `User Id`, `Password` y `Database` recuperados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="69df8-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="69df8-160">Aparecerá el símbolo del sistema MySQL:</span><span class="sxs-lookup"><span data-stu-id="69df8-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="69df8-161">Pegue el comando siguiente `CREATE TABLE` para crear la tabla `registration_tbl` en la base de datos:</span><span class="sxs-lookup"><span data-stu-id="69df8-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="69df8-162">En la raíz de la carpeta de la aplicación local, cree el archivo **index.php** .</span><span class="sxs-lookup"><span data-stu-id="69df8-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="69df8-163">Abra el archivo **index.php** en un editor de texto o entorno de desarrollo integrado y agregue el código siguiente. A continuación, realice los cambios necesarios marcados con comentarios `//TODO:`.</span><span class="sxs-lookup"><span data-stu-id="69df8-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="69df8-164">En un terminal, vaya a la carpeta de la aplicación y escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="69df8-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="69df8-165">Ahora puede ir a **http://localhost:8000/** para probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69df8-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="69df8-166">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="69df8-166">Publish your app</span></span>
<span data-ttu-id="69df8-167">Una vez que se haya probado la aplicación localmente, esta puede publicarse en Aplicaciones web mediante Git.</span><span class="sxs-lookup"><span data-stu-id="69df8-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="69df8-168">Será necesario inicializar el repositorio Git local y publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69df8-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="69df8-169">Estos son los mismos pasos que se muestran en el Portal de Azure al final de la sección Creación de una aplicación web y configuración de la publicación Git, más arriba.</span><span class="sxs-lookup"><span data-stu-id="69df8-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="69df8-170">(Opcional) Si ha olvidado la dirección URL del repositorio de Git remoto o no la encuentra, vaya a las propiedades de la aplicación web de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="69df8-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="69df8-171">Abra GitBash (o un terminal, si Git está en su `PATH`), cambie los directorios al directorio raíz de la aplicación y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="69df8-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="69df8-172">Se le solicitará la contraseña que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="69df8-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Inserción inicial en Azure a través de Git][git-initial-push]
3. <span data-ttu-id="69df8-174">Vaya a **http://[nombre del sitio].azurewebsites.net/index.php** para empezar a usar la aplicación (esta información se almacenará en el panel de la cuenta):</span><span class="sxs-lookup"><span data-stu-id="69df8-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Sitio web PHP de Azure][running-app]

<span data-ttu-id="69df8-176">Una vez publicada la aplicación, podrá comenzar a realizar cambios en esta y a usar Git para publicarlos.</span><span class="sxs-lookup"><span data-stu-id="69df8-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="69df8-177">Publicación de cambios de la aplicación</span><span class="sxs-lookup"><span data-stu-id="69df8-177">Publish changes to your app</span></span>
<span data-ttu-id="69df8-178">Para publicar los cambios de la aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="69df8-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="69df8-179">Realice los cambios en la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="69df8-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="69df8-180">Abra GitBash (o un terminal, si Git está en su `PATH`), cambie los directorios al directorio raíz de la aplicación y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="69df8-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="69df8-181">Se le solicitará la contraseña que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="69df8-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Inserción de cambios del sitio en Azure a través de Git][git-change-push]
3. <span data-ttu-id="69df8-183">Vaya a **http://[nombre del sitio].azurewebsites.net/index.php** para ver la aplicación y cualquier cambio realizado en esta:</span><span class="sxs-lookup"><span data-stu-id="69df8-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Sitio web PHP de Azure][running-app]

> [!NOTE]
> <span data-ttu-id="69df8-185">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de suscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="69df8-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="69df8-186">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="69df8-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="69df8-187">Habilitación de la automatización de Composer con la extensión Composer</span><span class="sxs-lookup"><span data-stu-id="69df8-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="69df8-188">De forma predeterminada, el proceso de implementación de git en el Servicio de aplicaciones no responde con composer.json, si tiene uno en el proyecto PHP.</span><span class="sxs-lookup"><span data-stu-id="69df8-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="69df8-189">Puede habilitar el procesamiento de composer.json durante `git push` si habilita la extensión Composer.</span><span class="sxs-lookup"><span data-stu-id="69df8-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="69df8-190">En la hoja de la aplicación web de PHP, en [Azure Portal][management-portal], haga clic en **Herramientas** > **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="69df8-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Configuración de la extensión Compositor][composer-extension-settings]
2. <span data-ttu-id="69df8-192">Haga clic en **Agregar** y, luego, en **Compositor**.</span><span class="sxs-lookup"><span data-stu-id="69df8-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Adición de la extensión Compositor][composer-extension-add]
3. <span data-ttu-id="69df8-194">Haga clic en **Aceptar** para aceptar las condiciones legales.</span><span class="sxs-lookup"><span data-stu-id="69df8-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="69df8-195">Haga clic de nuevo en **Aceptar** para agregar la extensión.</span><span class="sxs-lookup"><span data-stu-id="69df8-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="69df8-196">La hoja **Extensiones instaladas** mostrará ahora la extensión Compositor.</span><span class="sxs-lookup"><span data-stu-id="69df8-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="69df8-197">![Vista de la extensión Compositor][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="69df8-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="69df8-198">Ahora, ejecute `git add`, `git commit` y `git push` como en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="69df8-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="69df8-199">Verá que Composer está instalando las dependencias definidas en composer.json.</span><span class="sxs-lookup"><span data-stu-id="69df8-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Éxito de la extensión Compositor][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="69df8-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69df8-201">Next steps</span></span>
<span data-ttu-id="69df8-202">Para obtener más información, consulte el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="69df8-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
