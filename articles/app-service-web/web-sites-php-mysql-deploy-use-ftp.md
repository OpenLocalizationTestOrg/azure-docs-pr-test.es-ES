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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Creación de una aplicación web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP
En este tutorial se muestra cómo crear una aplicación web PHP-MySQL y cómo implementarla mediante FTP. En este tutorial se supone que dispone de [PHP][install-php], [MySQL][install-mysql], un servidor web y un cliente FTP instalado en el equipo. Las instrucciones de este tutorial se pueden seguir en cualquier sistema operativo, incluidos Windows, Mac y Linux. Una vez completada esta guía, tendrá una aplicación web PHP/MySQL que se ejecutará en Azure.

Aprenderá a:

* Crear una aplicación web y una base de datos MySQL con el Portal de Azure. Dado que PHP está habilitado en aplicaciones web de forma predeterminada, no existen requisitos especiales para ejecutar el código PHP.
* Publicar la aplicación en Azure mediante FTP.

Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP. La aplicación se hospedará en una aplicación web. A continuación se muestra una captura de pantalla de la aplicación completada:

![Sitio web PHP de Azure][running-app]

> [!NOTE]
> Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de registrarse para abrir una cuenta, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Creación de una aplicación web y configuración de la publicación FTP
Siga estos pasos para crear una aplicación web y una base de datos MySQL:

1. Inicie sesión en [Azure Portal][management-portal].
2. Haga clic en el icono **+Nuevo** de la parte superior izquierda del Portal de Azure.
   
    ![Crear un sitio web de Azure][new-website]
3. En la búsqueda, escriba **Aplicación web + MySQL** y haga clic en **Aplicación web + MySQL**.
   
    ![Crear un sitio web personalizado][custom-create]
4. Haga clic en **Crear**. Escriba un nombre de servicio de aplicaciones único, un nombre válido para el grupo de recursos y un nuevo plan de servicio.
   
    ![Establecer nombre de grupo de recurso][resource-group]
5. Especifique los valores para la nueva base de datos, incluida la aceptación de los términos legales.
   
    ![Crear una base de datos MySQL][new-mysql-db]
6. Una vez creada la aplicación web, verá la nueva hoja de servicio de aplicaciones.
7. Haga clic en **Configuración** > **Credenciales de implementación**. 
   
    ![Configurar credenciales de implementación][set-deployment-credentials]
8. Para habilitar la publicación FTP, debe proporcionar un nombre de usuario y una contraseña. Guarde las credenciales y tome nota del nombre de usuario y la contraseña que cree.
   
    ![Creación de credenciales de publicación][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Compilación y prueba local de la aplicación
Registration es una sencilla aplicación PHP que permite registrarse en un evento con solo proporcionar el nombre y la dirección de correo electrónico. La información de los usuarios inscritos anteriormente se muestra en una tabla. La información de registro se almacena en una base de datos MySQL. La aplicación consta de dos archivos:

* **index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.
* **createtable.php**: crea la tabla MySQL para la aplicación. Este archivo solo se usará una vez.

Para compilar y ejecutar la aplicación localmente, siga estos pasos. Tenga en cuenta que en estos pasos se presupone que tiene PHP, MySQL y un servidor web configurado en la máquina local, además de tener habilitada la [extensión PDO para MySQL][pdo-mysql].

1. Cree una base de datos MySQL llamada `registration`. Puede realizar este procedimiento desde el símbolo del sistema de MySQL con este comando:
   
        mysql> create database registration;
2. En el directorio raíz del servidor web, cree una carpeta llamada `registration` y dos archivos en ella: uno llamado `createtable.php` y otro `index.php`.
3. Abra el archivo `createtable.php` en un editor de texto o IDE y agregue el código siguiente. Este código se usará para crear la tabla `registration_tbl` en la base de datos `registration`.
   
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
   > Debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.
   > 
   > 
4. Abra un explorador web y vaya a [http://localhost/registration/createtable.php][localhost-createtable]. Esto creará la tabla `registration_tbl` en la base de datos.
5. Abra el archivo **index.php** en un editor de texto o IDE y agregue el código HTML y CSS básico para la página (el código de PHP se agregará en pasos posteriores).
   
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
6. En las etiquetas de PHP, agregue el código de PHP para la conexión a la base de datos.
   
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
   > De nuevo, debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.
   > 
   > 
7. Después del código de conexión a la base de datos, agregue el código para la inserción de información de registro en la base de datos.
   
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
8. Finalmente, después del código anterior, agregue el código para recuperar datos de la base de datos.
   
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

Ahora puede dirigirse a [http://localhost/registration/index.php][localhost-index] para probar la aplicación.

## <a name="get-mysql-and-ftp-connection-information"></a>Obtención de información de conexión de FTP y MySQL
Para conectarse a la base de datos MySQL que se ejecuta en aplicaciones web, necesita información de conexión. Si desea obtener la información de conexión de MySQL, siga estos pasos:

1. En la hoja de la aplicación web del servicio de aplicaciones, haga clic en el vínculo del grupo de recursos:
   
    ![Selección de grupo de recursos][select-resourcegroup]
2. En el grupo de recursos, haga clic en la base de datos:
   
    ![Seleccionar base de datos][select-database]
3. En el resumen de base de datos, seleccione **Configuración** > **Propiedades**.
   
    ![Seleccionar propiedades][select-properties]
4. Anote los valores de `Database`, `Host`, `User Id` y `Password`.
   
    ![Anotar propiedades][note-properties]
5. En la aplicación web, haga clic en el vínculo **Descargar perfil de publicación** situado en la esquina inferior derecha de la página:
   
    ![Descargar perfil de publicación][download-publish-profile]
6. Abra el archivo `.publishsettings` en un editor XML. 
7. Busque el elemento `<publishProfile >` con `publishMethod="FTP"` que se parece a lo siguiente:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Tome nota de los atributos `publishUrl`, `userName` y `userPWD` .

## <a name="publish-your-app"></a>Publicación de la aplicación
Una vez que se haya probado la aplicación localmente, esta puede publicarse en la aplicación web mediante FTP. Sin embargo, antes es necesario actualizar la información de la conexión a la base de datos en la aplicación. Con la información de conexión a la base de datos obtenida anteriormente (en la sección **Obtención de información de conexión de FTP y MySQL**), actualice la siguiente información en **ambos** archivos `createdatabase.php` y `index.php` con los valores adecuados:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Ahora está listo para publicar la aplicación mediante FTP.

1. Abra el cliente FTP que desee.
2. Especifique la *parte del nombre de host* del atributo `publishUrl` que anotó anteriormente en el cliente FTP.
3. Escriba sin modificar los atributos `userName` y `userPWD` que anotó anteriormente en el cliente FTP.
4. Establezca una conexión.

Una vez que haya conseguido conectarse, podrá cargar y descargar archivos según sea necesario. Asegúrese de que está cargando los archivos en el directorio raíz, que es `/site/wwwroot`.

Después de cargar `index.php` y `createtable.php`, vaya a **http://[nombre de sitio].azurewebsites.net/createtable.php** para crear una tabla MySQL para la aplicación y, a continuación, vaya a **http://[nombre sitio].azurewebsites.net/index.php** para comenzar a usar la aplicación.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, consulte el [Centro para desarrolladores de PHP](/develop/php/).

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

