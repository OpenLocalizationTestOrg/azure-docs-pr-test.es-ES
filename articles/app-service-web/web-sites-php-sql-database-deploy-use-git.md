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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Crear una aplicación web de PHP SQL e implementar tooAzure servicio de aplicaciones mediante Git
Este tutorial muestra cómo toocreate un PHP web app en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que conecta tooAzure base de datos SQL y cómo toodeploy con Git. Este tutorial se da por supuesto que tiene [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers para SQL Server para PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), y [Git] [ install-git] instalados en su equipo. Una vez completada esta guía, tendrá una aplicación web PHP-SQL que se ejecutará en Azure.

> [!NOTE]
> Puede instalar y configurar Microsoft Drivers de hello, SQL Server Express y PHP para SQL Server para PHP con hello [instalador de plataforma Web de Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Aprenderá a:

* Cómo toocreate una Azure web app y una base de datos SQL hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Como PHP está habilitado en la aplicación del servicio de aplicaciones Web de forma predeterminada, nada especial es toorun requiere el código PHP.
* ¿Cómo toopublish y volver a publicar el tooAzure de aplicación mediante Git.

Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP aplicación Hello se hospedará en un sitio Web de Azure. Una captura de pantalla de la aplicación hello completado es menor que:

![Sitio web PHP de Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Creación de una aplicación web de Azure y configuración de la publicación Git
Siga estos toocreate pasos una aplicación web de Azure y una base de datos de SQL:

1. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com/).
2. Abra hello Azure Marketplace, haga clic en hello **New** icono situado en la parte superior de hello izquierda del panel de hello, haga clic en **seleccionar todo** tooMarketplace y seleccione siguiente **Web y móvil**.
3. Hola Marketplace, seleccione **Web y móvil**.
4. Haga clic en hello **Web app + SQL** icono.
5. Después de leer la descripción de Hola de aplicación de hello Web + SQL aplicación, seleccione **crear**.
6. Haga clic en cada parte (**grupo de recursos**, **aplicación Web**, **base de datos**, y **suscripción**) y escriba o seleccione valores de hello necesarios campos:
   
   * Escriba un nombre de URL de su elección.    
   * Configuración de credenciales de servidor de bases de datos
   * Seleccione Hola región más cercana tooyou
     
     ![configurar su aplicación](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Cuando termine la definición de aplicación web de hello, haga clic en **crear**.
   
    Cuando se ha creado la aplicación web de hello, Hola **notificaciones** botón parpadeará en un color verde **correcto** y Hola tooshow abierto de hoja de grupo de recursos de ambos hello web hello y aplicación de base de datos SQL en el grupo de Hola.
8. Haga clic en el icono de la aplicación hello web en la hoja de hello recursos grupo hoja tooopen Hola aplicación web.
   
    ![Grupo de recursos de la aplicación web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. En **Configuración**, haga clic en **Implementación continua** > **Configurar los valores obligatorios**. Seleccione **Repositorio de Git local** y haga clic en **Aceptar**.
   
    ![Dónde está su código fuente](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Si no ha configurado antes un repositorio de Git, debe facilitar un nombre de usuario y una contraseña. toodo, haga clic en **configuración** > **las credenciales de implementación** de hoja de la aplicación hello web.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. En **configuración** haga clic en **propiedades** toosee Hola Git dirección URL remota que necesite toouse toodeploy la aplicación PHP más adelante.

## <a name="get-sql-database-connection-information"></a>Obtención de información de conexión de la Base de datos SQL
instancia de base de datos SQL de toohello tooconnect que está vinculada tooyour web app, su voluntad necesita Hola información de conexión, que especificó cuando creó la base de datos de Hola. Hola tooget información de conexión de base de datos SQL, siga estos pasos:

1. En la hoja del grupo de recursos de hello, haga clic en el icono de hello SQL la base de datos.
2. En la hoja de hello SQL la base de datos, haga clic en **configuración** > **propiedades**, a continuación, haga clic en **mostrar cadenas de conexión de base de datos**. 
   
    ![Ver las propiedades de una base de datos](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. De hello **PHP** sección del cuadro de diálogo resultante de hello, tome nota de los valores de hello para `Server`, `SQL Database`, y `User Name`. Usará estos valores más adelante al publicar su aplicación de web PHP tooAzure servicio de aplicaciones.

## <a name="build-and-test-your-application-locally"></a>Compilación y comprobación de la aplicación localmente
aplicación de registro de Hello es una sencilla aplicación de PHP que permite tooregister para un evento proporcionando su nombre y direcciones de correo. La información de los usuarios inscritos anteriormente se muestra en una tabla. La información de registro se almacena en una instancia de Base de datos SQL. aplicación Hello consta de dos archivos (copiar y pegar código disponible a continuación):

* **index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.
* **CreateTable.PHP**: crea la tabla de base de datos SQL de hello para la aplicación hello. Este archivo solo se usará una vez.

aplicación de hello toorun localmente, siga los pasos de Hola a continuación. Tenga en cuenta que estos pasos se supone tener PHP y SQL Server Express configurado en el equipo local y que se ha habilitado Hola [extensión PDO para SQL Server][pdo-sqlsrv].

1. Cree una base de datos de SQL Server denominada `registration`. Puede hacerlo desde hello `sqlcmd` símbolo del sistema con estos comandos:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. En el directorio raíz de la aplicación, cree dos archivos: uno llamado `createtable.php` y otro `index.php`.
3. Abra hello `createtable.php` un archivo en un editor de texto o IDE y agregar código de hello siguiente. Este código será usado toocreate hello `registration_tbl` tabla Hola `registration` base de datos.
   
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
   
    Tenga en cuenta que necesitará valores de hello tooupdate para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de SQL Server local y la contraseña.
4. En un terminal en directorio de raíz de Hola de Hola Hola de tipo de aplicación siguiente comando:
   
        php -S localhost:8000
5. Abra un explorador web y vaya demasiado**http://localhost:8000/createtable.php**. Esto creará hello `registration_tbl` tabla de base de datos de Hola.
6. Abra hello **index.php** un archivo en un editor de texto o IDE y agregue los código básico de HTML y CSS de hello para la página de hello (Hola código PHP se agregará en pasos posteriores).
   
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
7. Dentro de las etiquetas PHP hello, agregue el código PHP para la conexión de base de datos de toohello.
   
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
   
    De nuevo, se necesita valores de hello tooupdate para <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.
8. Código de conexión de base de datos de hello, siguiente, agregue código para insertar información de registro en la base de datos de Hola.
   
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
9. Finalmente, después de hello código anterior, agregue código para recuperar datos de la base de datos de Hola.
   
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

Ahora puede examinar demasiado**http://localhost:8000/index.php** aplicación de hello tootest.

## <a name="publish-your-application"></a>Publicación de la aplicación
Después de haber probado la aplicación localmente, se pueden publicar aplicaciones Web del servicio tooApp usando Git. Sin embargo, primero necesita información de conexión de base de datos de tooupdate hello en aplicación hello. Usando la información de conexión de base de datos de hello obtenido anteriormente (en hello **información de conexión de base de datos de SQL obtener** sección), Hola de actualización siguiente información en **ambos** hello `createdatabase.php` y `index.php` archivos con hello los valores adecuados:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> Hola <code>$host</code>, valor de saludo del servidor se debe anteponer con <code>tcp:</code>.
> 
> 

Ahora, está listo tooset la publicación de Git y publicar la aplicación hello.

> [!NOTE]
> Se trata de hello mismos pasos se indican al final de Hola de hello **crear una aplicación web de Azure y configurar la publicación de Git** sección anterior.
> 
> 

1. Abrir GitBash (o un terminal, si está Git en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación (hello **registro** directorio), y ejecución Hola siguiendo comandos:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Se le pedirá para contraseña de Hola que creó anteriormente.
2. Examinar demasiado**http://[web aplicación name].azurewebsites.net/createtable.php** tabla de base de datos SQL toocreate hello para la aplicación hello.
3. Examinar demasiado**http://[web aplicación name].azurewebsites.net/index.php** toobegin mediante la aplicación hello.

Después de publicar la aplicación, puede empezar a realizar cambios tooit y usar Git toopublish ellos. 

## <a name="publish-changes-tooyour-application"></a>Publicar aplicación de tooyour de cambios
toopublish cambia tooapplication, siga estos pasos:

1. Realizar cambios tooyour aplicación localmente.
2. Abra GitBash (o un terminal, TI Git está en su `PATH`), cambie el directorio de raíz de toohello de directorios de la aplicación y ejecutar Hola siguientes comandos:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Se le pedirá para contraseña de Hola que creó anteriormente.
3. Examinar demasiado**http://[web aplicación name].azurewebsites.net/index.php** toosee los cambios.

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

