---
title: "aaaCreate un MySQL PHP web de aplicación de servicio de aplicaciones de Azure y la implementación con Git"
description: "Un tutorial que muestra la aplicación que almacena los datos de MySQL web toocreate un PHP y el uso de tooAzure de implementación de Git."
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
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="3f141-103">Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante Git</span><span class="sxs-lookup"><span data-stu-id="3f141-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="3f141-104">Este tutorial muestra cómo toocreate un MySQL PHP de aplicación web y cómo toodeploy lo demasiado[servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) con Git.</span><span class="sxs-lookup"><span data-stu-id="3f141-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="3f141-105">Va a usar [PHP][install-php], Hola herramienta de línea de comandos de MySQL (parte de [MySQL][install-mysql]), y [Git] [ install-git] instalada en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3f141-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="3f141-106">instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo, incluidos Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="3f141-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="3f141-107">Una vez completada esta guía, tendrá una aplicación web PHP/MySQL que se ejecutará en Azure.</span><span class="sxs-lookup"><span data-stu-id="3f141-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="3f141-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="3f141-108">You will learn:</span></span>

* <span data-ttu-id="3f141-109">Cómo toocreate una aplicación web y un MySQL base de datos utilizando hello [Portal de Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3f141-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="3f141-110">Debido a PHP está habilitada en [aplicación del servicio de aplicaciones Web](http://go.microsoft.com/fwlink/?LinkId=529714) de forma predeterminada, nada especial es toorun requiere el código PHP.</span><span class="sxs-lookup"><span data-stu-id="3f141-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="3f141-111">¿Cómo toopublish y volver a publicar el tooAzure de aplicación mediante Git.</span><span class="sxs-lookup"><span data-stu-id="3f141-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="3f141-112">¿Cómo tooenable Hola compositor extensión tooautomate Compositor de tareas en cada `git push`.</span><span class="sxs-lookup"><span data-stu-id="3f141-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="3f141-113">Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP.</span><span class="sxs-lookup"><span data-stu-id="3f141-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="3f141-114">aplicación Hello se hospedará en aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="3f141-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="3f141-115">Una captura de pantalla de la aplicación hello completado es menor que:</span><span class="sxs-lookup"><span data-stu-id="3f141-115">A screenshot of hello completed application is below:</span></span>

![Sitio web PHP de Azure][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="3f141-117">Configurar el entorno de desarrollo de Hola</span><span class="sxs-lookup"><span data-stu-id="3f141-117">Set up hello development environment</span></span>
<span data-ttu-id="3f141-118">Este tutorial se da por supuesto que tiene [PHP][install-php], Hola herramienta de línea de comandos de MySQL (parte de [MySQL][install-mysql]), y [Git] [ install-git] instalados en su equipo.</span><span class="sxs-lookup"><span data-stu-id="3f141-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="3f141-119">Creación de una aplicación web y configuración de la publicación Git</span><span class="sxs-lookup"><span data-stu-id="3f141-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="3f141-120">Siga estos pasos toocreate una aplicación web y una base de datos de MySQL:</span><span class="sxs-lookup"><span data-stu-id="3f141-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="3f141-121">Inicio de sesión toohello [Portal de Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3f141-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="3f141-122">Haga clic en hello **New** icono.</span><span class="sxs-lookup"><span data-stu-id="3f141-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="3f141-123">Haga clic en **vea todos los** siguiente demasiado**Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="3f141-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="3f141-124">Haga clic en **Web + móvil** y, a continuación, en **Aplicación web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="3f141-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="3f141-125">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f141-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="3f141-126">Escriba un nombre válido para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3f141-126">Enter a valid name for your resource group.</span></span>
   
    ![Establecer nombre de grupo de recurso][resource-group]
6. <span data-ttu-id="3f141-128">Escriba valores para la nueva aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3f141-128">Enter values for your new web app.</span></span>
   
    ![Crear una aplicación web][new-web-app]
7. <span data-ttu-id="3f141-130">Especifique valores para la nueva base de datos, incluidos los acepta los términos legales toohello.</span><span class="sxs-lookup"><span data-stu-id="3f141-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Crear una base de datos MySQL][new-mysql-db]
8. <span data-ttu-id="3f141-132">Cuando se ha creado la aplicación web de hello, verá la nueva hoja de aplicación web Hola.</span><span class="sxs-lookup"><span data-stu-id="3f141-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="3f141-133">En **Configuración**, haga clic en **Implementación continua** y, a continuación, en *Configurar los valores obligatorios*.</span><span class="sxs-lookup"><span data-stu-id="3f141-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configuración de la publicación Git][setup-publishing]
10. <span data-ttu-id="3f141-135">Seleccione **repositorio de Git Local** para el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f141-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Configuración de un repositorio Git][setup-repository]
11. <span data-ttu-id="3f141-137">tooenable Git publicar, debe proporcionar un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="3f141-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="3f141-138">Tome nota Hola nombre de usuario y contraseña que cree.</span><span class="sxs-lookup"><span data-stu-id="3f141-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="3f141-139">(Si ya ha configurado un repositorio Git anteriormente, este paso se omitirá).</span><span class="sxs-lookup"><span data-stu-id="3f141-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Creación de credenciales de publicación][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="3f141-141">Obtención de información de la conexión MySQL remota</span><span class="sxs-lookup"><span data-stu-id="3f141-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="3f141-142">tooconnect toohello MySQL base de datos se ejecuta en las aplicaciones Web, su voluntad necesita Hola información de conexión.</span><span class="sxs-lookup"><span data-stu-id="3f141-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="3f141-143">tooget información de conexión de MySQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3f141-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="3f141-144">En el grupo de recursos, haga clic en base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="3f141-144">From your resource group, click hello database:</span></span>
   
    ![Seleccionar base de datos][select-database]
2. <span data-ttu-id="3f141-146">De base de datos de hello **configuración**, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="3f141-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Seleccionar propiedades][select-properties]
3. <span data-ttu-id="3f141-148">Tome nota de los valores de hello para `Database`, `Host`, `User Id`, y `Password`.</span><span class="sxs-lookup"><span data-stu-id="3f141-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Anotar propiedades][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="3f141-150">Compilación y prueba local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3f141-150">Build and test your app locally</span></span>
<span data-ttu-id="3f141-151">Ahora que ha creado una aplicación web, puede desarrollarla localmente e implementarla después de las pruebas.</span><span class="sxs-lookup"><span data-stu-id="3f141-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="3f141-152">aplicación de registro de Hello es una sencilla aplicación de PHP que permite tooregister para un evento proporcionando su nombre y direcciones de correo.</span><span class="sxs-lookup"><span data-stu-id="3f141-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="3f141-153">La información de los usuarios inscritos anteriormente se muestra en una tabla.</span><span class="sxs-lookup"><span data-stu-id="3f141-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="3f141-154">La información de registro se almacena en una base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="3f141-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="3f141-155">aplicación Hello consta de un archivo (copiar y pegar código disponible a continuación):</span><span class="sxs-lookup"><span data-stu-id="3f141-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="3f141-156">**index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.</span><span class="sxs-lookup"><span data-stu-id="3f141-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="3f141-157">toobuild y aplicación Hola ejecución localmente, siga los pasos de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="3f141-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="3f141-158">Tenga en cuenta que estos pasos se supone tener hello PHP y la herramienta de línea de comandos de MySQL (parte de MySQL) configurado en el equipo local, y que se ha habilitado hello [extensión PDO para MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="3f141-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="3f141-159">Conectar toohello remoto MySQL server con valor de Hola para `Data Source`, `User Id`, `Password`, y `Database` que recuperó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="3f141-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="3f141-160">Aparecerá la línea de comandos de MySQL de Hello:</span><span class="sxs-lookup"><span data-stu-id="3f141-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="3f141-161">Pegar en siguientes hello `CREATE TABLE` comando toocreate hello `registration_tbl` tabla en la base de datos:</span><span class="sxs-lookup"><span data-stu-id="3f141-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="3f141-162">En la raíz de hello de la carpeta de la aplicación local crear **index.php** archivo.</span><span class="sxs-lookup"><span data-stu-id="3f141-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="3f141-163">Abra hello **index.php** un archivo en un editor de texto o IDE y agregue Hola el siguiente código y los cambios necesarios de hello completa se marcan con `//TODO:` comentarios.</span><span class="sxs-lookup"><span data-stu-id="3f141-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
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

1. <span data-ttu-id="3f141-164">En una terminal tooyour vaya aplicación carpeta y el tipo hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3f141-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="3f141-165">Ahora puede examinar demasiado**http://localhost: 8000 /** aplicación de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="3f141-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="3f141-166">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3f141-166">Publish your app</span></span>
<span data-ttu-id="3f141-167">Después de haber probado la aplicación localmente, se pueden publicar aplicaciones de tooWeb con Git.</span><span class="sxs-lookup"><span data-stu-id="3f141-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="3f141-168">Debe inicializar el repositorio Git local y publicar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3f141-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="3f141-169">Estos son Hola mismos pasos que se muestran en hello Azure Portal final Hola de hello crear una aplicación web y establezca una publicación de Git sección anterior.</span><span class="sxs-lookup"><span data-stu-id="3f141-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="3f141-170">(Opcional)  Si ha olvidado o mal colocado la dirección URL de repositorio remoto de Git, navegue toohello propiedades de la aplicación web en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f141-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="3f141-171">Abra GitBash (o un terminal, si está Git en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación y ejecutar Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3f141-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="3f141-172">Se le pedirá para contraseña de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f141-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![TooAzure inicial de inserción a través de Git][git-initial-push]
3. <span data-ttu-id="3f141-174">Examinar demasiado**http://[site name].azurewebsites.net/index.php** toobegin mediante la aplicación hello (esta información se almacenará en el panel de cuenta):</span><span class="sxs-lookup"><span data-stu-id="3f141-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Sitio web PHP de Azure][running-app]

<span data-ttu-id="3f141-176">Después de publicar la aplicación, puede empezar a realizar cambios tooit y usar Git toopublish ellos.</span><span class="sxs-lookup"><span data-stu-id="3f141-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="3f141-177">Publicar aplicación de tooyour de cambios</span><span class="sxs-lookup"><span data-stu-id="3f141-177">Publish changes tooyour app</span></span>
<span data-ttu-id="3f141-178">toopublish cambios tooyour aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3f141-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="3f141-179">Realizar cambios tooyour aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="3f141-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="3f141-180">Abra GitBash (o un terminal, TI Git está en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación y ejecutar Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3f141-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="3f141-181">Se le pedirá para contraseña de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f141-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![Inserción de sitio Cambia tooAzure mediante Git][git-change-push]
3. <span data-ttu-id="3f141-183">Examinar demasiado**http://[site name].azurewebsites.net/index.php** toosee la aplicación y los cambios que haya hecho:</span><span class="sxs-lookup"><span data-stu-id="3f141-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Sitio web PHP de Azure][running-app]

> [!NOTE]
> <span data-ttu-id="3f141-185">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3f141-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3f141-186">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="3f141-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="3f141-187">Habilitar la automatización de compositor con hello extensión compositor</span><span class="sxs-lookup"><span data-stu-id="3f141-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="3f141-188">De forma predeterminada, proceso de implementación de git de hello en el servicio de aplicaciones no hace nada con composer.json, si dispone de uno en el proyecto PHP.</span><span class="sxs-lookup"><span data-stu-id="3f141-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="3f141-189">Puede habilitar composer.json procesamiento durante `git push` habilitando la extensión de hello compositor.</span><span class="sxs-lookup"><span data-stu-id="3f141-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="3f141-190">En su PHP web hoja de la aplicación Hola [portal de Azure][management-portal], haga clic en **herramientas** > **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="3f141-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Configuración de la extensión Compositor][composer-extension-settings]
2. <span data-ttu-id="3f141-192">Haga clic en **Agregar** y, luego, en **Compositor**.</span><span class="sxs-lookup"><span data-stu-id="3f141-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Adición de la extensión Compositor][composer-extension-add]
3. <span data-ttu-id="3f141-194">Haga clic en **Aceptar** tooaccept los términos legales.</span><span class="sxs-lookup"><span data-stu-id="3f141-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="3f141-195">Haga clic en **Aceptar** extensión Hola de tooadd nuevo.</span><span class="sxs-lookup"><span data-stu-id="3f141-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="3f141-196">Hola **extensiones instaladas** hoja mostrará ahora la extensión del compositor de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f141-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="3f141-197">![Vista de la extensión Compositor][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="3f141-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="3f141-198">Ahora, realizar `git add`, `git commit`, y `git push` al igual que en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f141-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="3f141-199">Verá que Composer está instalando las dependencias definidas en composer.json.</span><span class="sxs-lookup"><span data-stu-id="3f141-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Éxito de la extensión Compositor][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="3f141-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f141-201">Next steps</span></span>
<span data-ttu-id="3f141-202">Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="3f141-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
