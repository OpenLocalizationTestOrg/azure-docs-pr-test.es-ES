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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="bf673-103">Crear y conectar tooa base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="bf673-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="bf673-104">Este tutorial muestra cómo toocreate MySQL base de datos en hello [portal de Azure](https://portal.azure.com) (proveedor es [ClearDB](http://www.cleardb.com/)) y cómo tooconnect tooit desde un PHP web aplicación se ejecuta en [servicio de aplicaciones de Azure](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="bf673-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bf673-105">También puede crear una base de datos MySQL como parte de una [plantilla de aplicación de Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="bf673-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="bf673-106">Creación una base de datos MySQL en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bf673-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="bf673-107">toocreate una base de datos MySQL en el portal de Azure, Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="bf673-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="bf673-108">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf673-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bf673-109">Hola menú izquierdo, haga clic en **New** > **datos + almacenamiento** > **base de datos MySQL**.</span><span class="sxs-lookup"><span data-stu-id="bf673-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Creación una base de datos MySQL en Azure: inicio](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="bf673-111">Hola nueva base de datos de MySQL [hoja](azure-portal-overview.md), configurar la nueva base de datos de MySQL como sigue (*hoja*: una página de portal que se abre horizontalmente):</span><span class="sxs-lookup"><span data-stu-id="bf673-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="bf673-112">**Nombre de la base de datos**: escriba un nombre identificable de forma única.</span><span class="sxs-lookup"><span data-stu-id="bf673-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="bf673-113">**Suscripción**: elija Hola suscripción toouse</span><span class="sxs-lookup"><span data-stu-id="bf673-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="bf673-114">**Tipo base de datos**: seleccione **Shared** para los niveles de bajo costo o gratuito, o **dedicado** tooget recursos dedicados.</span><span class="sxs-lookup"><span data-stu-id="bf673-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="bf673-115">**Grupo de recursos**: agregar tooan existente de base de datos de MySQL de hello [grupo de recursos](azure-resource-manager/resource-group-overview.md) o colocarla en una nueva.</span><span class="sxs-lookup"><span data-stu-id="bf673-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="bf673-116">Recursos de hello mismo grupo se puede administrar fácilmente entre sí.</span><span class="sxs-lookup"><span data-stu-id="bf673-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="bf673-117">**Ubicación**: seleccione una tooyou de cierre de ubicación.</span><span class="sxs-lookup"><span data-stu-id="bf673-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="bf673-118">Al agregar tooan grupo de recursos existente, le ubicación del grupo de recursos de toohello bloqueado.</span><span class="sxs-lookup"><span data-stu-id="bf673-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="bf673-119">**Plan de tarifa**: haga clic en **Plan de tarifa**; después, seleccione una opción de precios (el nivel **Mercurio** es gratuito) y, luego, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="bf673-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="bf673-120">**Condiciones legales**: haga clic en **condiciones legales**, revise los detalles de la compra de Hola y haga clic en **comprar**.</span><span class="sxs-lookup"><span data-stu-id="bf673-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="bf673-121">**PIN toodashboard**: seleccione si desea tooaccess directamente desde el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf673-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="bf673-122">Esta opción le resultará especialmente útil si todavía se está familiarizando con la navegación por el Portal.</span><span class="sxs-lookup"><span data-stu-id="bf673-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="bf673-123">Hola siguiente captura de pantalla es simplemente un ejemplo de cómo puede configurar la base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf673-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Creación una base de datos MySQL en Azure: configuración](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="bf673-125">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bf673-125">When you're done configuring, click **Create**.</span></span>

    ![Creación una base de datos MySQL en Azure: creación](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="bf673-127">Verá una notificación emergente donde se le informará que se ha iniciado la implementación.</span><span class="sxs-lookup"><span data-stu-id="bf673-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Creación una base de datos MySQL en Azure: en curso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="bf673-129">Se mostrará otra ventana emergente cuando se complete correctamente la implementación.</span><span class="sxs-lookup"><span data-stu-id="bf673-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="bf673-130">portal de Hello también abrirá automáticamente la hoja de la base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf673-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="bf673-131">Conectar la base de datos de MySQL a tooyour</span><span class="sxs-lookup"><span data-stu-id="bf673-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="bf673-132">simplemente haga clic en la información de conexión de hello toosee para la nueva base de datos de MySQL, **propiedades** en la hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bf673-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Creación una base de datos MySQL en Azure: hoja Base de datos MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="bf673-134">Ahora puede emplear esa información de conexión en cualquier aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bf673-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="bf673-135">Un ejemplo que muestra cómo está disponible la información de conexión de hello toouse desde una aplicación sencilla de PHP [aquí](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="bf673-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="bf673-136">Conectar una aplicación web de Laravel (del tutorial introductorio de hello PHP get)</span><span class="sxs-lookup"><span data-stu-id="bf673-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="bf673-137">Suponga que el tutorial Hola simplemente terminado [crear, configurar e implementar una tooAzure de aplicación web PHP](app-service-web/app-service-web-php-get-started.md) y tener un [Laravel](https://www.laravel.com/) aplicación web que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="bf673-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="bf673-138">Puede agregar fácilmente aplicaciones de Laravel de tooyour de funciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="bf673-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="bf673-139">Sólo tiene que seguir estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="bf673-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="bf673-140">Hello siguientes pasos se supone que ha finalizado el tutorial de hello [crear, configurar e implementar una tooAzure de aplicación web PHP](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf673-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="bf673-141">Configurar aplicación Laravel de hello en la base de datos de MySQL de desarrollo local entorno toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="bf673-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="bf673-142">toodo, abra `.env` desde su aplicación Laravel directorio raíz y configurar las opciones de base de datos de MySQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf673-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="bf673-143">Hola **propiedades** hoja, puede nombre hello de la base de datos de MySQL o puede no ser Hola uno se muestra en hello **nombre de base de datos** campo.</span><span class="sxs-lookup"><span data-stu-id="bf673-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="bf673-144">Es mejor parámetro de base de datos de hello toocheck Hola **cadena de conexión** campo.</span><span class="sxs-lookup"><span data-stu-id="bf673-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Creación una base de datos MySQL en Azure: en curso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="bf673-146">Hola tooverify de manera más rápida que ahora tiene acceso de MySQL es toouse [scaffolding de autenticación predeterminada del Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="bf673-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="bf673-147">En el terminal de línea de comandos de hello, ejecute hello siguientes comandos de directorio raíz de la aplicación Laravel:</span><span class="sxs-lookup"><span data-stu-id="bf673-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="bf673-148">Hola primer comando crea tablas de hello en Azure basado en migraciones predefinidas en hello `database/migrations` directorio y segundo comando de hello scaffolds Hola vistas básicas y rutas para el registro de usuario y la autenticación.</span><span class="sxs-lookup"><span data-stu-id="bf673-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="bf673-149">Ejecute ahora el servidor de desarrollo de hello:</span><span class="sxs-lookup"><span data-stu-id="bf673-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="bf673-150">En el Explorador de hello, navegue toohttp://localhost:8000 y registrar un nuevo usuario como se muestra:</span><span class="sxs-lookup"><span data-stu-id="bf673-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Conectar la base de datos de tooMySQL en Azure: registrar al usuario](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="bf673-152">Siga el registro de mensajes hello completa de interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf673-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="bf673-153">Cuando se haya registrado, se iniciará la sesión.</span><span class="sxs-lookup"><span data-stu-id="bf673-153">Once registration completes, you will be logged in.</span></span>

    ![Conectar la base de datos de tooMySQL en Azure: registrar al usuario](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="bf673-155">Ahora está desarrollando la aplicación en la base de datos de MySQL de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="bf673-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="bf673-156">Ahora, solo necesita tooreplicate su `.env` aplicación de configuración tooyour web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf673-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="bf673-157">Ejecute hello siga los comandos de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="bf673-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="bf673-158">A continuación, confirme e inserte cambios locales de tooAzure Hola realizados anteriormente mientras se está ejecutando `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="bf673-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="bf673-159">Busque la aplicación web de Azure de toohello.</span><span class="sxs-lookup"><span data-stu-id="bf673-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="bf673-160">Inicie sesión con credenciales de usuario de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bf673-160">Log in using hello user credentials you created earlier.</span></span>

    ![Conectar la base de datos de tooMySQL en Azure: examinar la aplicación web de tooAzure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="bf673-162">Después de iniciar sesión, debería ver la pantalla de bienvenida descriptivo posterior a la de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bf673-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Conectar tooMySQL base de datos de Azure: iniciado sesión](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="bf673-164">Enhorabuena. La aplicación web PHP de Azure ahora tiene acceso a datos de la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="bf673-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf673-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf673-165">Next steps</span></span>
<span data-ttu-id="bf673-166">Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="bf673-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
