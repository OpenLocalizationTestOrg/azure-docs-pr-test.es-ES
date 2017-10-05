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
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a>Crear una aplicación web de PHP-SQL e implementarla en el Servicio de aplicaciones de Azure mediante Git
En este tutorial se muestra cómo crear una aplicación web PHP en el [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) que se conecta a Base de datos SQL de Azure y cómo implementarla mediante Git. En este tutorial se supone que tiene [PHP][install-php], [SQL Server Express][install-SQLExpress], [controladores de Microsoft para SQL Server para PHP](http://www.microsoft.com/download/en/details.aspx?id=20098) y [Git][install-git] instalados en el equipo. Una vez completada esta guía, tendrá una aplicación web PHP-SQL que se ejecutará en Azure.

> [!NOTE]
> Puede instalar y configurar PHP, SQL Server Express, los controladores de Microsoft para SQL Server para PHP mediante el [instalador de plataforma web de Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Aprenderá a:

* Creación de una aplicación web de Azure y una base de datos SQL mediante el [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Dado que PHP está habilitado en Aplicaciones web del Servicio de aplicaciones de forma predeterminada, no existen requisitos especiales para ejecutar el código PHP.
* Publicar y volver a publicar la aplicación en Azure con Git.

Mediante este tutorial, se compilará una aplicación web de registro sencilla en PHP que se hospedará en un sitio web de Azure. Captura de pantalla de la aplicación completa:

![Sitio web PHP de Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Creación de una aplicación web de Azure y configuración de la publicación Git
Siga estos pasos para crear una aplicación web de Azure y una base de datos SQL:

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).
2. Abra Azure Marketplace haciendo clic en el icono **Nuevo** situado en la parte superior izquierda del panel, haga clic en **Seleccionar todo** junto a Marketplace y seleccione **Web + móvil**.
3. En Marketplace, elija **Web + móvil**.
4. Haga clic en el icono **Aplicación web + SQL** .
5. Después de leer la descripción de la aplicación web + SQL, elija **Crear**.
6. Haga clic en cada parte (**Grupo de recursos**, **Aplicación web**, **Base de datos** y **Suscripción**) y escriba o seleccione los valores para los campos obligatorios:
   
   * Escriba un nombre de URL de su elección.    
   * Configuración de credenciales de servidor de bases de datos
   * Seleccione la región más cercana a la suya.
     
     ![configurar su aplicación](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Cuando termine de definir la aplicación web, haga clic en **Crear**.
   
    Una vez creada la aplicación web, el botón **Notificaciones** emitirá el mensaje **Correcto** en color verde y la hoja del grupo de recursos se abrirá para mostrar la aplicación web y la base de datos SQL en el grupo.
8. Haga clic en el icono de la hoja del grupo de recursos para abrirla.
   
    ![Grupo de recursos de la aplicación web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. En **Configuración**, haga clic en **Implementación continua** > **Configurar los valores obligatorios**. Seleccione **Repositorio de Git local** y haga clic en **Aceptar**.
   
    ![Dónde está su código fuente](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Si no ha configurado antes un repositorio de Git, debe facilitar un nombre de usuario y una contraseña. Para ello, haga clic en **Configuración** > **Credenciales de implementación** en la hoja de la aplicación web.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. En **Configuración**, haga clic en **Propiedades** para ver la dirección URL remota de Git que necesita para implementar la aplicación PHP más adelante.

## <a name="get-sql-database-connection-information"></a>Obtención de información de conexión de la Base de datos SQL
Para conectarse a la instancia de Base de datos SQL vinculada a la aplicación web, necesitará la información de conexión que especificó al crear la base de datos. Para obtener la información de conexión de Base de datos SQL, siga estos pasos:

1. En la hoja del grupo de recursos, haga clic en el icono de Base de datos SQL.
2. En la hoja de Base de datos SQL, haga clic en **Configuración** > **Propiedades** y, luego, en **Mostrar cadenas de conexión de la base de datos**. 
   
    ![Ver las propiedades de una base de datos](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. En la sección **PHP** del cuadro de diálogo que aparece, anote los valores de `Server`, `SQL Database` y `User Name`. Usará estos valores más adelante al publicar la aplicación web PHP en el Servicio de aplicaciones de Azure.

## <a name="build-and-test-your-application-locally"></a>Compilación y comprobación de la aplicación localmente
Registration es una sencilla aplicación PHP que permite registrarse en un evento con solo proporcionar el nombre y la dirección de correo electrónico. La información de los usuarios inscritos anteriormente se muestra en una tabla. La información de registro se almacena en una instancia de Base de datos SQL. La aplicación se compone de dos archivos (código para copiar y pegar disponible más abajo):

* **index.php**: muestra un formulario de registro y una tabla que contiene la información de los usuarios inscritos.
* **createtable.php**: crea la tabla de Base de datos SQL para la aplicación. Este archivo solo se usará una vez.

Para ejecutar la aplicación localmente, realice los pasos siguientes. Tenga en cuenta que en estos pasos se supone que tiene PHP y SQL Server Express configurados en la máquina local, además de tener habilitada la [extensión PDO para SQL Server][pdo-sqlsrv].

1. Cree una base de datos de SQL Server denominada `registration`. Puede realizar este procedimiento desde el símbolo del sistema `sqlcmd` con estos comandos:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. En el directorio raíz de la aplicación, cree dos archivos: uno llamado `createtable.php` y otro `index.php`.
3. Abra el archivo `createtable.php` en un editor de texto o IDE y agregue el código siguiente. Este código se usará para crear la tabla `registration_tbl` en la base de datos `registration`.
   
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
   
    Tenga en cuenta que debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de SQL Server local y la contraseña.
4. En un terminal en el directorio raíz de la aplicación, escriba el siguiente comando:
   
        php -S localhost:8000
5. Abra un explorador web y vaya a **http://localhost:8000/createtable.php**. Esto creará la tabla `registration_tbl` en la base de datos.
6. Abra el archivo **index.php** en un editor de texto o IDE y agregue el código HTML y CSS básico para la página (el código de PHP se agregará en pasos posteriores).
   
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
7. En las etiquetas de PHP, agregue el código de PHP para la conexión a la base de datos.
   
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
   
    De nuevo, debe actualizar los valores de <code>$user</code> y <code>$pwd</code> con su nombre de usuario de MySQL local y la contraseña.
8. Después del código de conexión a la base de datos, agregue el código para la inserción de información de registro en la base de datos.
   
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
9. Finalmente, después del código anterior, agregue el código para recuperar datos de la base de datos.
   
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

Ahora puede ir a **http://localhost:8000/index.php** para probar la aplicación.

## <a name="publish-your-application"></a>Publicación de la aplicación
Una vez que se haya probado la aplicación localmente, puede publicarla en Aplicaciones web del servicio de aplicaciones mediante Git. Sin embargo, antes es necesario actualizar la información de la conexión a la base de datos en la aplicación. Con la información de conexión a la base de datos obtenida anteriormente (en la sección **Obtención de información de conexión de SQL**), actualice la siguiente información en **ambos** archivos `createdatabase.php` y `index.php` con los valores adecuados:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> En el <code>$host</code>, el valor de servidor se debe anteponer con <code>tcp:</code>.
> 
> 

Ahora, está listo para configurar la publicación de Git y publicar la aplicación.

> [!NOTE]
> Estos son los mismos pasos que se indican al final de la sección **Creación de una aplicación web de Azure y configuración de la publicación Git** , más arriba.
> 
> 

1. Abra GitBash (o un terminal, si Git está en su `PATH`), cambie los directorios al directorio raíz de la aplicación (el directorio de **registro** )y ejecute los siguientes comandos:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Se le solicitará la contraseña que ha creado anteriormente.
2. Vaya a **http://[nombre de aplicación web].azurewebsites.net/createtable.php** para crear la tabla de Base de datos SQL para la aplicación.
3. Vaya a **http://[nombre de aplicación web].azurewebsites.net/index.php** para comenzar a usar la aplicación.

Una vez publicada la aplicación, podrá comenzar a realizar cambios en esta y a usar Git para publicarlos. 

## <a name="publish-changes-to-your-application"></a>Publicación de cambios de la aplicación
Para publicar los cambios de la aplicación, siga estos pasos:

1. Realice los cambios en la aplicación localmente.
2. Abra GitBash (o un terminal, si Git está en su `PATH`), cambie los directorios al directorio raíz de la aplicación y ejecute los siguientes comandos:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Se le solicitará la contraseña que ha creado anteriormente.
3. Vaya a **http://[nombre de aplicación web].azurewebsites.net/index.php** para ver los cambios.

## <a name="whats-changed"></a>Lo que ha cambiado
* Para obtener una guía del cambio de Websites a App Service, consulte: [Azure App Service y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

