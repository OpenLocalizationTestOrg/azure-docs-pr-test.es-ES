---
title: "aaaCreate y conéctese tooa base de datos MySQL en Azure"
description: "Obtenga información acerca de cómo toouse Hola toocreate portal Azure una base de datos MySQL y, a continuación, conectarse tooit desde una aplicación web PHP en Azure."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Crear y conectar tooa base de datos MySQL en Azure
Este tutorial muestra cómo toocreate MySQL base de datos en hello [portal de Azure](https://portal.azure.com) (proveedor es [ClearDB](http://www.cleardb.com/)) y cómo tooconnect tooit desde un PHP web aplicación se ejecuta en [servicio de aplicaciones de Azure](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> También puede crear una base de datos MySQL como parte de una [plantilla de aplicación de Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Creación una base de datos MySQL en el Portal de Azure
toocreate una base de datos MySQL en el portal de Azure, Hola Hola siguientes:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola menú izquierdo, haga clic en **New** > **datos + almacenamiento** > **base de datos MySQL**.

    ![Creación una base de datos MySQL en Azure: inicio](./media/store-php-create-mysql-database/create-db-1-start.png)
3. Hola nueva base de datos de MySQL [hoja](azure-portal-overview.md), configurar la nueva base de datos de MySQL como sigue (*hoja*: una página de portal que se abre horizontalmente):

   * **Nombre de la base de datos**: escriba un nombre identificable de forma única.
   * **Suscripción**: elija Hola suscripción toouse
   * **Tipo base de datos**: seleccione **Shared** para los niveles de bajo costo o gratuito, o **dedicado** tooget recursos dedicados.
   * **Grupo de recursos**: agregar tooan existente de base de datos de MySQL de hello [grupo de recursos](azure-resource-manager/resource-group-overview.md) o colocarla en una nueva. Recursos de hello mismo grupo se puede administrar fácilmente entre sí.
   * **Ubicación**: seleccione una tooyou de cierre de ubicación. Al agregar tooan grupo de recursos existente, le ubicación del grupo de recursos de toohello bloqueado.
   * **Plan de tarifa**: haga clic en **Plan de tarifa**; después, seleccione una opción de precios (el nivel **Mercurio** es gratuito) y, luego, haga clic en **Seleccionar**.
   * **Condiciones legales**: haga clic en **condiciones legales**, revise los detalles de la compra de Hola y haga clic en **comprar**.
   * **PIN toodashboard**: seleccione si desea tooaccess directamente desde el panel de Hola. Esta opción le resultará especialmente útil si todavía se está familiarizando con la navegación por el Portal.

     Hola siguiente captura de pantalla es simplemente un ejemplo de cómo puede configurar la base de datos de MySQL.  
     ![Creación una base de datos MySQL en Azure: configuración](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Cuando haya terminado, haga clic en **Crear**.

    ![Creación una base de datos MySQL en Azure: creación](./media/store-php-create-mysql-database/create-db-3-create.png)

    Verá una notificación emergente donde se le informará que se ha iniciado la implementación.

    ![Creación una base de datos MySQL en Azure: en curso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Se mostrará otra ventana emergente cuando se complete correctamente la implementación. portal de Hello también abrirá automáticamente la hoja de la base de datos de MySQL.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Conectar la base de datos de MySQL a tooyour
simplemente haga clic en la información de conexión de hello toosee para la nueva base de datos de MySQL, **propiedades** en la hoja de la aplicación web.

![Creación una base de datos MySQL en Azure: hoja Base de datos MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Ahora puede emplear esa información de conexión en cualquier aplicación web. Un ejemplo que muestra cómo está disponible la información de conexión de hello toouse desde una aplicación sencilla de PHP [aquí](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Conectar una aplicación web de Laravel (del tutorial introductorio de hello PHP get)
Suponga que el tutorial Hola simplemente terminado [crear, configurar e implementar una tooAzure de aplicación web PHP](app-service-web/app-service-web-php-get-started.md) y tener un [Laravel](https://www.laravel.com/) aplicación web que se ejecuta en Azure. Puede agregar fácilmente aplicaciones de Laravel de tooyour de funciones de base de datos. Sólo tiene que seguir estos pasos hello:

> [!NOTE]
> Hello siguientes pasos se supone que ha finalizado el tutorial de hello [crear, configurar e implementar una tooAzure de aplicación web PHP](app-service-web/app-service-web-php-get-started.md).
>
>

1. Configurar aplicación Laravel de hello en la base de datos de MySQL de desarrollo local entorno toopoint toohello. toodo, abra `.env` desde su aplicación Laravel directorio raíz y configurar las opciones de base de datos de MySQL de Hola.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > Hola **propiedades** hoja, puede nombre hello de la base de datos de MySQL o puede no ser Hola uno se muestra en hello **nombre de base de datos** campo. Es mejor parámetro de base de datos de hello toocheck Hola **cadena de conexión** campo.    
   >
   > ![Creación una base de datos MySQL en Azure: en curso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Hola tooverify de manera más rápida que ahora tiene acceso de MySQL es toouse [scaffolding de autenticación predeterminada del Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   En el terminal de línea de comandos de hello, ejecute hello siguientes comandos de directorio raíz de la aplicación Laravel:

         php artisan migrate
         php artisan make:auth

    Hola primer comando crea tablas de hello en Azure basado en migraciones predefinidas en hello `database/migrations` directorio y segundo comando de hello scaffolds Hola vistas básicas y rutas para el registro de usuario y la autenticación.
3. Ejecute ahora el servidor de desarrollo de hello:

        php artisan serve
4. En el Explorador de hello, navegue toohttp://localhost:8000 y registrar un nuevo usuario como se muestra:

    ![Conectar la base de datos de tooMySQL en Azure: registrar al usuario](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Siga el registro de mensajes hello completa de interfaz de usuario de Hola. Cuando se haya registrado, se iniciará la sesión.

    ![Conectar la base de datos de tooMySQL en Azure: registrar al usuario](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Ahora está desarrollando la aplicación en la base de datos de MySQL de hello en Azure.
5. Ahora, solo necesita tooreplicate su `.env` aplicación de configuración tooyour web de Azure. Ejecute hello siga los comandos de CLI de Azure:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. A continuación, confirme e inserte cambios locales de tooAzure Hola realizados anteriormente mientras se está ejecutando `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Busque la aplicación web de Azure de toohello.

        azure site browse
8. Inicie sesión con credenciales de usuario de Hola que creó anteriormente.

    ![Conectar la base de datos de tooMySQL en Azure: examinar la aplicación web de tooAzure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Después de iniciar sesión, debería ver la pantalla de bienvenida descriptivo posterior a la de inicio de sesión.

    ![Conectar tooMySQL base de datos de Azure: iniciado sesión](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Enhorabuena. La aplicación web PHP de Azure ahora tiene acceso a datos de la base de datos MySQL.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).
