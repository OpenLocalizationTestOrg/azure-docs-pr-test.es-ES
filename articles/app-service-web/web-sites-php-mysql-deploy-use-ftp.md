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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP
Este tutorial muestra cómo toocreate un MySQL PHP de aplicación web y cómo toodeploy a través de FTP. En este tutorial se supone que dispone de [PHP][install-php], [MySQL][install-mysql], un servidor web y un cliente FTP instalado en el equipo. instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo, incluidos Windows, Mac y Linux. Una vez completada esta guía, tendrá una aplicación web PHP/MySQL que se ejecutará en Azure.

Aprenderá a:

* Cómo toocreate una aplicación web y un MySQL base de datos utilizando Hola Portal de Azure. Como PHP está habilitado en las aplicaciones Web de forma predeterminada, nada especial es toorun requiere el código PHP.
* Cómo toopublish tooAzure aplicación mediante FTP.

Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP. aplicación Hello se hospeda en una aplicación Web. Una captura de pantalla de la aplicación hello completado es menor que:

![Sitio web PHP de Azure][running-app]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Creación de una aplicación web y configuración de la publicación FTP
Siga estos pasos toocreate una aplicación web y una base de datos de MySQL:

1. Inicio de sesión toohello [Portal de Azure][management-portal].
2. Haga clic en hello **+ nuevo** icono situado en la parte superior de hello izquierda de hello Portal de Azure.
   
    ![Crear un sitio web de Azure][new-website]
3. En el tipo de búsqueda de hello **Web app + MySQL** y haga clic en **Web app + MySQL**.
   
    ![Crear un sitio web personalizado][custom-create]
4. Haga clic en **Crear**. Escriba un nombre de servicio de aplicaciones único, un nombre válido para el grupo de recursos de Hola y un nuevo plan de servicio.
   
    ![Establecer nombre de grupo de recurso][resource-group]
5. Especifique valores para la nueva base de datos, incluidos los acepta los términos legales toohello.
   
    ![Crear una base de datos MySQL][new-mysql-db]
6. Cuando se ha creado la aplicación web de hello, verá la nueva hoja de servicio de aplicación Hola.
7. Haga clic en **Configuración** > **Credenciales de implementación**. 
   
    ![Configurar credenciales de implementación][set-deployment-credentials]
8. tooenable publicación FTP, debe proporcionar un nombre de usuario y una contraseña. Guardar las credenciales de Hola y tome nota del nombre de usuario de Hola y la contraseña que se crea.
   
    ![Creación de credenciales de publicación][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Compilación y prueba local de la aplicación
aplicación de registro de Hello es una sencilla aplicación de PHP que permite tooregister para un evento proporcionando su nombre y direcciones de correo. La información de los usuarios inscritos anteriormente se muestra en una tabla. La información de registro se almacena en una base de datos MySQL. aplicación Hello consta de dos archivos:

* **index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.
* **CreateTable.PHP**: crea la tabla de MySQL de hello para la aplicación hello. Este archivo solo se usará una vez.

toobuild y aplicación de hello ejecución localmente, siga los pasos de hello siguientes. Tenga en cuenta que estos pasos se supone que tiene PHP, MySQL y un servidor web configurado en el equipo local y que se ha habilitado Hola [extensión PDO para MySQL][pdo-mysql].

1. Cree una base de datos MySQL llamada `registration`. Puede hacerlo desde la línea de comandos de MySQL Hola con este comando:
   
        mysql> create database registration;
2. En el directorio raíz del servidor web, cree una carpeta llamada `registration` y dos archivos en ella: uno llamado `createtable.php` y otro `index.php`.
3. Abra hello `createtable.php` un archivo en un editor de texto o IDE y agregar código de hello siguiente. Este código será usado toocreate hello `registration_tbl` tabla Hola `registration` base de datos.
   
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
   > Necesitará tooupdate Hola valores para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.
   > 
   > 
4. Abra un explorador web y vaya demasiado[http://localhost/registration/createtable.php][localhost-createtable]. Esto creará hello `registration_tbl` tabla de base de datos de Hola.
5. Abra hello **index.php** un archivo en un editor de texto o IDE y agregue los código básico de HTML y CSS de hello para la página de hello (Hola código PHP se agregará en pasos posteriores).
   
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
6. Dentro de las etiquetas PHP hello, agregue el código PHP para la conexión de base de datos de toohello.
   
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
   > De nuevo, se necesita valores de hello tooupdate para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.
   > 
   > 
7. Código de conexión de base de datos de hello, siguiente, agregue código para insertar información de registro en la base de datos de Hola.
   
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
8. Finalmente, después de hello código anterior, agregue código para recuperar datos de la base de datos de Hola.
   
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

Ahora puede examinar demasiado[http://localhost/registration/index.php] [ localhost-index] tootest Hola aplicación.

## <a name="get-mysql-and-ftp-connection-information"></a>Obtención de información de conexión de FTP y MySQL
tooconnect toohello MySQL base de datos se ejecuta en las aplicaciones Web, su voluntad necesita Hola información de conexión. tooget información de conexión de MySQL, siga estos pasos:

1. De servicio de aplicaciones de hello hoja de la aplicación web, haga clic en el vínculo de grupo de recursos de hello:
   
    ![Selección de grupo de recursos][select-resourcegroup]
2. En el grupo de recursos, haga clic en base de datos de hello:
   
    ![Seleccionar base de datos][select-database]
3. En la base de datos de hello resumen, seleccione **configuración** > **propiedades**.
   
    ![Seleccionar propiedades][select-properties]
4. Tome nota de los valores de hello para `Database`, `Host`, `User Id`, y `Password`.
   
    ![Anotar propiedades][note-properties]
5. Desde la aplicación web, haga clic en hello **descargar perfil de publicación** en hello esquina inferior derecha de la página de hello vínculo:
   
    ![Descargar perfil de publicación][download-publish-profile]
6. Abra hello `.publishsettings` archivo en un editor XML. 
7. Buscar hello `<publishProfile >` elemento con `publishMethod="FTP"` que busca toothis similar:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Tome nota de hello `publishUrl`, `userName`, y `userPWD` atributos.

## <a name="publish-your-app"></a>Publicación de la aplicación
Después de haber probado la aplicación localmente, puede publicarlo tooyour web app mediante FTP. Sin embargo, primero necesita información de conexión de base de datos de tooupdate hello en aplicación hello. Usando la información de conexión de base de datos de hello obtenido anteriormente (en hello **información de conexión FTP y obtener MySQL** sección), Hola de actualización siguiente información en **ambos** hello `createdatabase.php` y `index.php` archivos con hello los valores adecuados:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Ahora está listo toopublish su aplicación mediante FTP.

1. Abra el cliente FTP que desee.
2. Escriba hello *parte del nombre de host* de hello `publishUrl` atributo indicados anteriormente en el cliente FTP.
3. Escriba hello `userName` y `userPWD` sin modificar atributos mencionados anteriormente en el cliente FTP.
4. Establezca una conexión.

Después de haberse conectado se ser capaz de tooupload y descargar archivos según sea necesario. Asegúrese de que esté cargando el directorio raíz de toohello de archivos, que es `/site/wwwroot`.

Después de cargar ambos `index.php` y `createtable.php`, examinar demasiado**http://[site name].azurewebsites.net/createtable.php** toocreate Hola MySQL de la tabla de la aplicación hello, a continuación, examinar demasiado**http://[site nombre ].azurewebsites.net/index.php** toobegin mediante la aplicación hello.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).

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

