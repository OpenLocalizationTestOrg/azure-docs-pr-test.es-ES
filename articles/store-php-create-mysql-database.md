---
title: "Creación y conexión de una base de datos MySQL en Azure"
description: "Obtenga información sobre cómo usar el Portal de Azure para crear una base de datos MySQL y, después, conectarse a ella desde una aplicación web PHP en Azure."
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
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="5c635-103">Creación y conexión de una base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="5c635-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="5c635-104">En este tutorial se le enseñará a crear una base de datos MySQL en [Azure Portal](https://portal.azure.com) (el proveedor es [ClearDB](http://www.cleardb.com/)) y cómo conectarse a ella desde una aplicación web PHP que se ejecute en [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="5c635-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5c635-105">También puede crear una base de datos MySQL como parte de una [plantilla de aplicación de Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="5c635-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="5c635-106">Creación una base de datos MySQL en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5c635-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="5c635-107">Para restaurar una base de datos MySQL en el Portal de Azure, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c635-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="5c635-108">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c635-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c635-109">En el menú izquierdo, haga clic en **Nuevo** > **Datos y almacenamiento** > **Base de datos MySQL**.</span><span class="sxs-lookup"><span data-stu-id="5c635-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Creación una base de datos MySQL en Azure: inicio](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="5c635-111">En la [hoja](azure-portal-overview.md)Nueva base de datos MySQL, configure la nueva base de datos MySQL tal y como se muestra a continuación (*hoja*: una página del Portal que se abre horizontalmente):</span><span class="sxs-lookup"><span data-stu-id="5c635-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="5c635-112">**Nombre de la base de datos**: escriba un nombre identificable de forma única.</span><span class="sxs-lookup"><span data-stu-id="5c635-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="5c635-113">**Suscripción**: elija la suscripción que va a utilizar</span><span class="sxs-lookup"><span data-stu-id="5c635-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="5c635-114">**Tipo de base de datos**: seleccione **Compartido** para los niveles de bajo coste o gratuitos, o bien **Dedicado** si desea obtener recursos específicos.</span><span class="sxs-lookup"><span data-stu-id="5c635-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="5c635-115">**Grupo de recursos**: agregue la base de datos MySQL a un [grupo de recursos](azure-resource-manager/resource-group-overview.md) existente, o bien colóquela en uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="5c635-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="5c635-116">Los recursos del mismo grupo pueden administrarse juntos de manera sencilla.</span><span class="sxs-lookup"><span data-stu-id="5c635-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="5c635-117">**Ubicación**: elija una ubicación cercana a usted.</span><span class="sxs-lookup"><span data-stu-id="5c635-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="5c635-118">Cuando se agrega la base de datos a un grupo de recursos existente, no podrá acceder a la ubicación de este.</span><span class="sxs-lookup"><span data-stu-id="5c635-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="5c635-119">**Plan de tarifa**: haga clic en **Plan de tarifa**; después, seleccione una opción de precios (el nivel **Mercurio** es gratuito) y, luego, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="5c635-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="5c635-120">**Condiciones legales**: haga clic en **Condiciones legales**, revise los detalles de la compra y haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="5c635-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="5c635-121">**Anclar al panel**: seleccione si desea acceder directamente desde el panel.</span><span class="sxs-lookup"><span data-stu-id="5c635-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="5c635-122">Esta opción le resultará especialmente útil si todavía se está familiarizando con la navegación por el Portal.</span><span class="sxs-lookup"><span data-stu-id="5c635-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="5c635-123">La siguiente captura de pantalla es tan solo un ejemplo de cómo puede configurar la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c635-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Creación una base de datos MySQL en Azure: configuración](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="5c635-125">Cuando haya terminado, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5c635-125">When you're done configuring, click **Create**.</span></span>

    ![Creación una base de datos MySQL en Azure: creación](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="5c635-127">Verá una notificación emergente donde se le informará que se ha iniciado la implementación.</span><span class="sxs-lookup"><span data-stu-id="5c635-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Creación una base de datos MySQL en Azure: en curso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="5c635-129">Se mostrará otra ventana emergente cuando se complete correctamente la implementación.</span><span class="sxs-lookup"><span data-stu-id="5c635-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="5c635-130">El Portal también abrirá automáticamente la hoja de la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c635-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="5c635-131">Conexión a la base de datos MySQL</span><span class="sxs-lookup"><span data-stu-id="5c635-131">Connect to your MySQL database</span></span>
<span data-ttu-id="5c635-132">Para ver la información de conexión de la nueva base de datos MySQL, haga clic en **Propiedades** en la hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5c635-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Creación una base de datos MySQL en Azure: hoja Base de datos MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="5c635-134">Ahora puede emplear esa información de conexión en cualquier aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5c635-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="5c635-135">[Aquí](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)puede encontrar un ejemplo que muestra cómo utilizar la información de conexión de una aplicación PHP simple.</span><span class="sxs-lookup"><span data-stu-id="5c635-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="5c635-136">Conexión de una aplicación web de Laravel (del tutorial de introducción de PHP)</span><span class="sxs-lookup"><span data-stu-id="5c635-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="5c635-137">Si, por ejemplo, acaba de finalizar el tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) (Creación, configuración e implementación de aplicaciones web PHP en Azure) y tiene una aplicación web de [Laravel](https://www.laravel.com/) que se ejecuta en Azure,</span><span class="sxs-lookup"><span data-stu-id="5c635-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="5c635-138">podrá agregar fácilmente las funcionalidades de base de datos a la aplicación Laravel.</span><span class="sxs-lookup"><span data-stu-id="5c635-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="5c635-139">Siga los pasos que se indican a continuación:</span><span class="sxs-lookup"><span data-stu-id="5c635-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="5c635-140">En los siguientes pasos se da por hecho que ha finalizado la tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md)(Creación, configuración e implementación de aplicaciones web PHP en Azure).</span><span class="sxs-lookup"><span data-stu-id="5c635-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="5c635-141">Configure la aplicación Laravel en su entorno de desarrollo local para que apunte a la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c635-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="5c635-142">Para ello, abra `.env` desde el directorio raíz de la aplicación Laravel y configure las opciones de base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c635-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="5c635-143">En la hoja **Propiedades**, puede que no se muestre el nombre de la base de datos MySQL en el campo **NOMBRE DE LA BASE DE DATOS**.</span><span class="sxs-lookup"><span data-stu-id="5c635-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="5c635-144">Se recomienda comprobar el parámetro Database del campo **CADENA DE CONEXIÓN** .</span><span class="sxs-lookup"><span data-stu-id="5c635-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Creación una base de datos MySQL en Azure: en curso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="5c635-146">La forma más rápida de comprobar que ahora tiene acceso a MySQL es usar la técnica [scaffolding de autenticación predeterminada de Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="5c635-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="5c635-147">En el terminal de la línea de comandos, ejecute los siguientes comandos desde el directorio raíz de la aplicación Laravel:</span><span class="sxs-lookup"><span data-stu-id="5c635-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="5c635-148">El primer comando crea las tablas en Azure según las migraciones predefinidas del directorio `database/migrations`, mientras que el segundo comando aplica la técnica scaffolding en las vistas básicas y las rutas de autenticación y registro de usuarios.</span><span class="sxs-lookup"><span data-stu-id="5c635-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="5c635-149">Ejecute ahora el servidor de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="5c635-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="5c635-150">En el explorador, vaya a http://localhost:8000 y registre un nuevo usuario tal y como se muestra:</span><span class="sxs-lookup"><span data-stu-id="5c635-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Conexión a la base de datos MySQL en Azure: registro de usuarios](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="5c635-152">Siga las indicaciones de la interfaz de usuario para completar el registro.</span><span class="sxs-lookup"><span data-stu-id="5c635-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="5c635-153">Cuando se haya registrado, se iniciará la sesión.</span><span class="sxs-lookup"><span data-stu-id="5c635-153">Once registration completes, you will be logged in.</span></span>

    ![Conexión a la base de datos MySQL en Azure: registro de usuarios](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="5c635-155">Ahora está desarrollando la aplicación en la base de datos MySQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c635-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="5c635-156">Ahora, solo tiene que replicar la configuración de `.env` en la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c635-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="5c635-157">Ejecute los siguientes comandos de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="5c635-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="5c635-158">Después, confirme y envíe a Azure los cambios locales realizados anteriormente durante la ejecución de `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="5c635-158">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="5c635-159">Vaya a la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c635-159">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="5c635-160">Inicie sesión con las credenciales de usuario que creó antes.</span><span class="sxs-lookup"><span data-stu-id="5c635-160">Log in using the user credentials you created earlier.</span></span>

    ![Conexión a la base de datos MySQL en Azure: acceso a la aplicación web de Azure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="5c635-162">Después de iniciar sesión, deberá ver la pantalla posterior a este paso, con una intuitiva interfaz.</span><span class="sxs-lookup"><span data-stu-id="5c635-162">After you log in, you should see the friendly post-login screen.</span></span>

    ![Conexión a la base de datos MySQL en Azure: sesión iniciada](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="5c635-164">Enhorabuena. La aplicación web PHP de Azure ahora tiene acceso a datos de la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c635-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c635-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c635-165">Next steps</span></span>
<span data-ttu-id="5c635-166">Para obtener más información, consulte el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5c635-166">For more information, see the [PHP Developer Center](/develop/php/).</span></span>
