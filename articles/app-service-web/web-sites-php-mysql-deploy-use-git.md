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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante Git
Este tutorial muestra cómo toocreate un MySQL PHP de aplicación web y cómo toodeploy lo demasiado[servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) con Git. Va a usar [PHP][install-php], Hola herramienta de línea de comandos de MySQL (parte de [MySQL][install-mysql]), y [Git] [ install-git] instalada en el equipo. instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo, incluidos Windows, Mac y Linux. Una vez completada esta guía, tendrá una aplicación web PHP/MySQL que se ejecutará en Azure.

Aprenderá a:

* Cómo toocreate una aplicación web y un MySQL base de datos utilizando hello [Portal de Azure][management-portal]. Debido a PHP está habilitada en [aplicación del servicio de aplicaciones Web](http://go.microsoft.com/fwlink/?LinkId=529714) de forma predeterminada, nada especial es toorun requiere el código PHP.
* ¿Cómo toopublish y volver a publicar el tooAzure de aplicación mediante Git.
* ¿Cómo tooenable Hola compositor extensión tooautomate Compositor de tareas en cada `git push`.

Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP. aplicación Hello se hospedará en aplicaciones Web. Una captura de pantalla de la aplicación hello completado es menor que:

![Sitio web PHP de Azure][running-app]

## <a name="set-up-hello-development-environment"></a>Configurar el entorno de desarrollo de Hola
Este tutorial se da por supuesto que tiene [PHP][install-php], Hola herramienta de línea de comandos de MySQL (parte de [MySQL][install-mysql]), y [Git] [ install-git] instalados en su equipo.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Creación de una aplicación web y configuración de la publicación Git
Siga estos pasos toocreate una aplicación web y una base de datos de MySQL:

1. Inicio de sesión toohello [Portal de Azure][management-portal].
2. Haga clic en hello **New** icono.
3. Haga clic en **vea todos los** siguiente demasiado**Marketplace**. 
4. Haga clic en **Web + móvil** y, a continuación, en **Aplicación web + MySQL**. A continuación, haga clic en **Crear**.
5. Escriba un nombre válido para el grupo de recursos.
   
    ![Establecer nombre de grupo de recurso][resource-group]
6. Escriba valores para la nueva aplicación web.
   
    ![Crear una aplicación web][new-web-app]
7. Especifique valores para la nueva base de datos, incluidos los acepta los términos legales toohello.
   
    ![Crear una base de datos MySQL][new-mysql-db]
8. Cuando se ha creado la aplicación web de hello, verá la nueva hoja de aplicación web Hola.
9. En **Configuración**, haga clic en **Implementación continua** y, a continuación, en *Configurar los valores obligatorios*.
   
    ![Configuración de la publicación Git][setup-publishing]
10. Seleccione **repositorio de Git Local** para el origen de Hola.
    
     ![Configuración de un repositorio Git][setup-repository]
11. tooenable Git publicar, debe proporcionar un nombre de usuario y una contraseña. Tome nota Hola nombre de usuario y contraseña que cree. (Si ya ha configurado un repositorio Git anteriormente, este paso se omitirá).
    
     ![Creación de credenciales de publicación][credentials]

## <a name="get-remote-mysql-connection-information"></a>Obtención de información de la conexión MySQL remota
tooconnect toohello MySQL base de datos se ejecuta en las aplicaciones Web, su voluntad necesita Hola información de conexión. tooget información de conexión de MySQL, siga estos pasos:

1. En el grupo de recursos, haga clic en base de datos de hello:
   
    ![Seleccionar base de datos][select-database]
2. De base de datos de hello **configuración**, seleccione **propiedades**.
   
    ![Seleccionar propiedades][select-properties]
3. Tome nota de los valores de hello para `Database`, `Host`, `User Id`, y `Password`.
   
    ![Anotar propiedades][note-properties]

## <a name="build-and-test-your-app-locally"></a>Compilación y prueba local de la aplicación
Ahora que ha creado una aplicación web, puede desarrollarla localmente e implementarla después de las pruebas.

aplicación de registro de Hello es una sencilla aplicación de PHP que permite tooregister para un evento proporcionando su nombre y direcciones de correo. La información de los usuarios inscritos anteriormente se muestra en una tabla. La información de registro se almacena en una base de datos MySQL. aplicación Hello consta de un archivo (copiar y pegar código disponible a continuación):

* **index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.

toobuild y aplicación Hola ejecución localmente, siga los pasos de hello siguientes. Tenga en cuenta que estos pasos se supone tener hello PHP y la herramienta de línea de comandos de MySQL (parte de MySQL) configurado en el equipo local, y que se ha habilitado hello [extensión PDO para MySQL][pdo-mysql].

1. Conectar toohello remoto MySQL server con valor de Hola para `Data Source`, `User Id`, `Password`, y `Database` que recuperó anteriormente:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. Aparecerá la línea de comandos de MySQL de Hello:
   
        mysql>
3. Pegar en siguientes hello `CREATE TABLE` comando toocreate hello `registration_tbl` tabla en la base de datos:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. En la raíz de hello de la carpeta de la aplicación local crear **index.php** archivo.
5. Abra hello **index.php** un archivo en un editor de texto o IDE y agregue Hola el siguiente código y los cambios necesarios de hello completa se marcan con `//TODO:` comentarios.

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

1. En una terminal tooyour vaya aplicación carpeta y el tipo hello siguiente comando:
   
       php -S localhost:8000

Ahora puede examinar demasiado**http://localhost: 8000 /** aplicación de hello tootest.

## <a name="publish-your-app"></a>Publicación de la aplicación
Después de haber probado la aplicación localmente, se pueden publicar aplicaciones de tooWeb con Git. Debe inicializar el repositorio Git local y publicar la aplicación hello.

> [!NOTE]
> Estos son Hola mismos pasos que se muestran en hello Azure Portal final Hola de hello crear una aplicación web y establezca una publicación de Git sección anterior.
> 
> 

1. (Opcional)  Si ha olvidado o mal colocado la dirección URL de repositorio remoto de Git, navegue toohello propiedades de la aplicación web en hello Portal de Azure.
2. Abra GitBash (o un terminal, si está Git en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación y ejecutar Hola siguientes comandos:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Se le pedirá para contraseña de Hola que creó anteriormente.
   
    ![TooAzure inicial de inserción a través de Git][git-initial-push]
3. Examinar demasiado**http://[site name].azurewebsites.net/index.php** toobegin mediante la aplicación hello (esta información se almacenará en el panel de cuenta):
   
    ![Sitio web PHP de Azure][running-app]

Después de publicar la aplicación, puede empezar a realizar cambios tooit y usar Git toopublish ellos.

## <a name="publish-changes-tooyour-app"></a>Publicar aplicación de tooyour de cambios
toopublish cambios tooyour aplicación, siga estos pasos:

1. Realizar cambios tooyour aplicación localmente.
2. Abra GitBash (o un terminal, TI Git está en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación y ejecutar Hola siguientes comandos:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Se le pedirá para contraseña de Hola que creó anteriormente.
   
    ![Inserción de sitio Cambia tooAzure mediante Git][git-change-push]
3. Examinar demasiado**http://[site name].azurewebsites.net/index.php** toosee la aplicación y los cambios que haya hecho:
   
    ![Sitio web PHP de Azure][running-app]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>Habilitar la automatización de compositor con hello extensión compositor
De forma predeterminada, proceso de implementación de git de hello en el servicio de aplicaciones no hace nada con composer.json, si dispone de uno en el proyecto PHP. Puede habilitar composer.json procesamiento durante `git push` habilitando la extensión de hello compositor.

1. En su PHP web hoja de la aplicación Hola [portal de Azure][management-portal], haga clic en **herramientas** > **extensiones**.
   
    ![Configuración de la extensión Compositor][composer-extension-settings]
2. Haga clic en **Agregar** y, luego, en **Compositor**.
   
    ![Adición de la extensión Compositor][composer-extension-add]
3. Haga clic en **Aceptar** tooaccept los términos legales. Haga clic en **Aceptar** extensión Hola de tooadd nuevo.
   
    Hola **extensiones instaladas** hoja mostrará ahora la extensión del compositor de Hola.  
    ![Vista de la extensión Compositor][composer-extension-view]
4. Ahora, realizar `git add`, `git commit`, y `git push` al igual que en la sección anterior de Hola. Verá que Composer está instalando las dependencias definidas en composer.json.
   
    ![Éxito de la extensión Compositor][composer-extension-success]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).

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
