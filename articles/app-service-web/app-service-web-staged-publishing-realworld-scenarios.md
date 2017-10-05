---
title: Uso eficaz de entornos DevOps para las aplicaciones web | Microsoft Docs
description: "Aprenda a usar ranuras de implementación para configurar y administrar varios entornos de desarrollo para la aplicación"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="58023-103">Uso eficaz de entornos DevOps para las aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="58023-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="58023-104">En este artículo se muestra cómo configurar y administrar implementaciones de aplicaciones web cuando hay varias versiones de la aplicación en diversos entornos, como desarrollo, ensayo, control de calidad (QA) y producción.</span><span class="sxs-lookup"><span data-stu-id="58023-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="58023-105">Cada versión de la aplicación puede considerarse como un entorno de desarrollo para la finalidad específica de su proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="58023-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="58023-106">Por ejemplo, los desarrolladores pueden usar el entorno de QA para probar la calidad de la aplicación antes de insertar los cambios en producción.</span><span class="sxs-lookup"><span data-stu-id="58023-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="58023-107">El uso de varios entornos de desarrollo puede presentar dificultades, dado que debe realizar el seguimiento del código, administrar los recursos (proceso, aplicación web, base de datos, caché, etc.) e implementar código entre entornos.</span><span class="sxs-lookup"><span data-stu-id="58023-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="58023-108">Configuración de un entorno que no es de producción (ensayo, desarrollo, control de calidad)</span><span class="sxs-lookup"><span data-stu-id="58023-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="58023-109">Una vez que la aplicación web de producción está en funcionamiento, el siguiente paso consiste en crear un entorno que no sea de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="58023-110">Para usar espacios de implementación, asegúrese de estar ejecutando el modo del plan Estándar o Premium de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="58023-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="58023-111">Los espacios de implementación son aplicaciones web activas que tienen sus propios nombres de host.</span><span class="sxs-lookup"><span data-stu-id="58023-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="58023-112">Los elementos de contenido y configuración de aplicaciones web se pueden intercambiar entre dos espacios de implementación, incluida la ranura de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="58023-113">Cuando implementa la aplicación en un espacio de implementación, obtiene las ventajas siguientes:</span><span class="sxs-lookup"><span data-stu-id="58023-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="58023-114">Puede validar los cambios en la aplicación web en un espacio de implementación de ensayo antes de intercambiar la aplicación con el espacio de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="58023-115">Cuando implementa una aplicación web en un espacio en primer lugar y después la intercambia con producción, todas las instancias del espacio están correctas antes de colocarse en producción.</span><span class="sxs-lookup"><span data-stu-id="58023-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="58023-116">Este proceso elimina tiempos de inactividad al implementar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="58023-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="58023-117">El redireccionamiento del tráfico es impecable y no se anulan las solicitudes como consecuencia de las operaciones de intercambio.</span><span class="sxs-lookup"><span data-stu-id="58023-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="58023-118">Para automatizar este flujo de trabajo completo, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) (Intercambio automático) cuando no se necesite la validación antes del intercambio.</span><span class="sxs-lookup"><span data-stu-id="58023-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="58023-119">Después de un intercambio, el espacio que contenía la aplicación web tiene ahora la aplicación web de producción anterior.</span><span class="sxs-lookup"><span data-stu-id="58023-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="58023-120">Si los cambios intercambiados con el espacio de producción no son los esperados, puede realizar el mismo intercambio inmediatamente para volver a la "última aplicación web buena conocida".</span><span class="sxs-lookup"><span data-stu-id="58023-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="58023-121">Para configurar una ranura de implementación de ensayo, consulte [Configuración de entornos de ensayo para aplicaciones web en Azure App Service](web-sites-staged-publishing.md) .</span><span class="sxs-lookup"><span data-stu-id="58023-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="58023-122">Todos los entornos deberían incluir su conjunto de recursos propio.</span><span class="sxs-lookup"><span data-stu-id="58023-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="58023-123">Por ejemplo, si la aplicación web utiliza una base de datos, las aplicaciones web de producción y de ensayo deben usar bases de datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="58023-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="58023-124">Agregue recursos de entorno de desarrollo de ensayo, como una base de datos, almacenamiento o caché, para configurar el entorno de desarrollo de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="58023-125">Ejemplos del uso de varios entornos de desarrollo</span><span class="sxs-lookup"><span data-stu-id="58023-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="58023-126">Cualquier proyecto debería poner en práctica la administración de código fuente con al menos dos entornos: desarrollo y producción.</span><span class="sxs-lookup"><span data-stu-id="58023-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="58023-127">Si usa sistemas de administración de contenido (CMS), marcos de aplicaciones, etc., es posible que la aplicación no admita este escenario sin personalización.</span><span class="sxs-lookup"><span data-stu-id="58023-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="58023-128">Esta posibilidad es aplicable a algunos de los marcos de trabajo habituales que se describen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="58023-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="58023-129">Vienen a la mente muchas preguntas cuando se trabaja con CMS o marcos, como por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="58023-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="58023-130">¿Cómo se extrae el contenido y se introduce en entornos diferentes?</span><span class="sxs-lookup"><span data-stu-id="58023-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="58023-131">¿Qué archivos se pueden cambiar sin afectar a las actualizaciones de versión del marco?</span><span class="sxs-lookup"><span data-stu-id="58023-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="58023-132">¿Cómo se administran las configuraciones para cada entorno?</span><span class="sxs-lookup"><span data-stu-id="58023-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="58023-133">¿Cómo se administran las actualizaciones de versión de módulos, complementos y el marco de trabajo principal?</span><span class="sxs-lookup"><span data-stu-id="58023-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="58023-134">Existen muchas maneras de configurar varios entornos para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="58023-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="58023-135">En los ejemplos siguientes, se muestra un método para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="58023-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="58023-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="58023-136">WordPress</span></span>
<span data-ttu-id="58023-137">En esta sección, obtendrá información sobre cómo configurar un flujo de trabajo de implementación mediante espacios para WordPress.</span><span class="sxs-lookup"><span data-stu-id="58023-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="58023-138">WordPress, al igual que la mayoría de las soluciones CMS, no admite varios entornos de desarrollo sin llevar a cabo personalización.</span><span class="sxs-lookup"><span data-stu-id="58023-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="58023-139">La característica Web Apps de Azure App Service incluye algunas características que facilitan el almacenamiento de la configuración fuera del código.</span><span class="sxs-lookup"><span data-stu-id="58023-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="58023-140">Antes de crear un espacio de ensayo, configure el código de la aplicación para admita varios entornos.</span><span class="sxs-lookup"><span data-stu-id="58023-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="58023-141">Para admitir varios entornos en WordPress, debe editar `wp-config.php` en la aplicación web de desarrollo local y agregar el código siguiente al principio del archivo.</span><span class="sxs-lookup"><span data-stu-id="58023-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="58023-142">Este proceso permitirá que la aplicación seleccione la configuración correcta en función del entorno seleccionado.</span><span class="sxs-lookup"><span data-stu-id="58023-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

    ```
    // Support multiple environments
    // set the config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="58023-143">Cree una carpeta bajo la raíz de la aplicación web llamada `config` y agregue los archivos `wp-config.azure.php` y `wp-config.local.php`, que representan el entorno de Azure y el entorno local, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="58023-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="58023-144">Copie lo siguiente en `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="58023-144">Copy the following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    <span data-ttu-id="58023-145">Establecer las claves de seguridad como se muestra en el código anterior puede ayudar a evitar que se piratee la aplicación web, así que debería usar valores únicos.</span><span class="sxs-lookup"><span data-stu-id="58023-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="58023-146">Si debe generar la cadena para las claves de seguridad mencionadas en el código, puede [ir al generador automático](https://api.wordpress.org/secret-key/1.1/salt) para crear pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="58023-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="58023-147">Copie el siguiente código en `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="58023-147">Copy the following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a><span data-ttu-id="58023-148">Uso de rutas de acceso relativas</span><span class="sxs-lookup"><span data-stu-id="58023-148">Use relative paths</span></span>
<span data-ttu-id="58023-149">Lo último que hay que configurar en la aplicación de WordPress son las rutas de acceso relativas.</span><span class="sxs-lookup"><span data-stu-id="58023-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="58023-150">WordPress almacena la información de dirección URL en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="58023-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="58023-151">Este almacenamiento dificulta el traslado de contenido de un entorno a otro.</span><span class="sxs-lookup"><span data-stu-id="58023-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="58023-152">Debe actualizar la base de datos cada vez que se mueva del entorno local al de ensayo, o del de ensayo al de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="58023-153">Para reducir el riesgo de que surjan problemas que pueden deberse a la implementación de la base de datos cada vez que se pasa de un entorno a otro, use el [complemento de vínculos relativos a la raíz](https://wordpress.org/plugins/root-relative-urls/), que se puede instalar mediante el panel de administrador de WordPress.</span><span class="sxs-lookup"><span data-stu-id="58023-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="58023-154">Agregue las siguientes entradas al archivo `wp-config.php` delante del comentario `That's all, stop editing!`:</span><span class="sxs-lookup"><span data-stu-id="58023-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="58023-155">Active el complemento en el menú `Plugins` del panel de administrador de WordPress.</span><span class="sxs-lookup"><span data-stu-id="58023-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="58023-156">Guarde la configuración de vínculo permanente para la aplicación de WordPress.</span><span class="sxs-lookup"><span data-stu-id="58023-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="58023-157">El archivo `wp-config.php` final</span><span class="sxs-lookup"><span data-stu-id="58023-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="58023-158">Las actualizaciones principales de WordPress no afectan a los archivos `wp-config.php`, `wp-config.azure.php` ni `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="58023-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="58023-159">Esta es una versión final del archivo `wp-config.php`:</span><span class="sxs-lookup"><span data-stu-id="58023-159">Here's a final version of the `wp-config.php` file:</span></span>

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="58023-160">Configuración de un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="58023-160">Set up a staging environment</span></span>
1. <span data-ttu-id="58023-161">Si ya tiene ejecutándose una aplicación web de WordPress en su suscripción de Azure, inicie sesión en [Azure Portal](http://portal.azure.com)y vaya a la aplicación web de WordPress.</span><span class="sxs-lookup"><span data-stu-id="58023-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="58023-162">Si carece de aplicación web de WordPress, puede crearla desde Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="58023-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="58023-163">Para más información, consulte [Creación de una aplicación web de WordPress en Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="58023-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="58023-164">Haga clic en **Settings** > **Deployment slots** > **Add** (Configuración > Espacios de implementación > Agregar) para crear un espacio de implementación llamado *stage*.</span><span class="sxs-lookup"><span data-stu-id="58023-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="58023-165">Un espacio de implementación es otra aplicación web que comparte los mismos recursos que la aplicación web principal creada antes.</span><span class="sxs-lookup"><span data-stu-id="58023-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Creación de la ranura de implementación de ensayo](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="58023-167">Agregue otra base de datos MySQL, como `wordpress-stage-db`, al grupo de recursos `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="58023-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![Incorporación de una base de datos de MySQL a un grupo de recursos](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="58023-169">Actualice las cadenas de conexión para el espacio de implementación de ensayo de forma que apunten a la nueva base de datos, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="58023-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="58023-170">La aplicación web de producción, `wordpressprodapp`, y la aplicación web de ensayo, `wordpressprodapp-stage`, deben apuntar a bases de datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="58023-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="58023-171">Configuración de valores de aplicación específicos del entorno</span><span class="sxs-lookup"><span data-stu-id="58023-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="58023-172">Los desarrolladores pueden almacenar pares clave-valor en Azure como parte de la información de configuración, llamada **App Settings** (Configuración de aplicación), que está asociada con una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="58023-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="58023-173">En tiempo de ejecución, las aplicaciones web recuperan automáticamente estos valores y los ponen a disposición del código que se ejecuta en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="58023-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="58023-174">Desde el punto de vista de la seguridad, esto resulta beneficioso, ya que la información confidencial, como las cadenas de conexión de base de datos que incluyen contraseñas, no se muestran nunca sin cifrar en un archivo como `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="58023-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="58023-175">Este proceso, que se explica en los párrafos siguientes, es útil porque incluye cambios tanto de archivo como de base de datos para la aplicación de WordPress:</span><span class="sxs-lookup"><span data-stu-id="58023-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="58023-176">Actualización de versión de WordPress</span><span class="sxs-lookup"><span data-stu-id="58023-176">WordPress version upgrade</span></span>
* <span data-ttu-id="58023-177">Agregar nuevos complementos, o bien editar o actualizar los existentes</span><span class="sxs-lookup"><span data-stu-id="58023-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="58023-178">Agregar nuevos temas o editar o actualizar los existentes</span><span class="sxs-lookup"><span data-stu-id="58023-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="58023-179">Configure los valores de aplicación para:</span><span class="sxs-lookup"><span data-stu-id="58023-179">Configure app settings for:</span></span>

* <span data-ttu-id="58023-180">Información de base de datos</span><span class="sxs-lookup"><span data-stu-id="58023-180">Database information</span></span>
* <span data-ttu-id="58023-181">Activar o desactivar el registro de WordPress</span><span class="sxs-lookup"><span data-stu-id="58023-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="58023-182">Configurar la seguridad de WordPress</span><span class="sxs-lookup"><span data-stu-id="58023-182">WordPress security settings</span></span>

![Configuración de aplicaciones para la aplicación web de Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="58023-184">Asegúrese de agregar la siguiente configuración de aplicación para el espacio de ensayo y la aplicación web de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="58023-185">Tenga en cuenta que la aplicación web de producción y la de ensayo usan diferentes bases de datos.</span><span class="sxs-lookup"><span data-stu-id="58023-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="58023-186">Desactive la casilla **Slot Setting** (Configuración de espacios) para todos los parámetros de configuración, excepto WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="58023-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="58023-187">Este proceso cambiara la configuración de la aplicación web, del contenido del archivo y de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="58023-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="58023-188">Si se activa **Slot Setting** (Configuración de espacios), la configuración de aplicación y la configuración de cadena de conexión de la aplicación web *no* se moverá entre entornos cuando se realice una operación de **intercambio**.</span><span class="sxs-lookup"><span data-stu-id="58023-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="58023-189">Los cambios de base de datos que estén presentes no interrumpirán la aplicación web de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="58023-190">Implemente la aplicación web del entorno de desarrollo local en la aplicación web y la base de datos de ensayo mediante WebMatrix u otra herramienta de su elección, como FTP, Git o PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="58023-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Cuadro de diálogo de publicación de WebMatrix para una aplicación web de WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="58023-192">Examine y pruebe la aplicación web provisional.</span><span class="sxs-lookup"><span data-stu-id="58023-192">Browse and test your staging web app.</span></span> <span data-ttu-id="58023-193">Si consideramos un escenario en el que se va actualizar el tema de la aplicación web, esta sería la aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Examen de la aplicación web de ensayo antes del intercambio de ranuras](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="58023-195">Si todo está bien, haga clic en el botón **Swap** (Intercambiar) en la aplicación web de ensayo para mover el contenido al entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="58023-196">En este caso, intercambia la aplicación web y la base de datos entre entornos durante cada operación de **intercambio**.</span><span class="sxs-lookup"><span data-stu-id="58023-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Vista previa de los cambios de intercambio para WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="58023-198">Si su escenario solo necesita insertar archivos (sin actualizaciones de la base de datos), active la casilla **Slot Setting** (Configuración de espacios) para todos los *valores de configuración de aplicación* y de *configuración de cadenas de conexión* que estén relacionados con la base de datos en la hoja **Web App Settings** (Configuración de aplicación web), en Azure Portal, antes de realizar el **intercambio**.</span><span class="sxs-lookup"><span data-stu-id="58023-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="58023-199">En este caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER y la configuración predeterminada de cadena de conexión no deberían aparecer en los cambios de versión preliminar cuando realice un **intercambio**.</span><span class="sxs-lookup"><span data-stu-id="58023-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="58023-200">En este momento, cuando finalice la operación de **intercambio**, la aplicación web de WordPress solo tendrá los archivos de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="58023-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="58023-201">Antes de realizar un **intercambio**, la aplicación web de WordPress de producción es esta.</span><span class="sxs-lookup"><span data-stu-id="58023-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="58023-202">![Aplicación web de producción antes del intercambio de espacios](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="58023-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="58023-203">Después de la operación de **intercambio**, el tema se actualiza en la aplicación web de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![Aplicación web de producción después del intercambio de ranuras](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="58023-205">En una situación en que necesite revertir a una versión anterior, puede ir a **App Settings** (Configuración de aplicación) para la aplicación web de producción y hacer clic en el botón **Swap** (Intercambiar) para cambiar la aplicación web y la base de datos del espacio de producción al de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="58023-206">Recuerde que si se incluyen los cambios de base de datos con una operación de **intercambio**, la próxima vez que implemente en la aplicación web de ensayo, debe implementar los cambios de la base de datos en la base de datos actual de la aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="58023-207">La base de datos podría ser la base de datos de producción anterior o la de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="58023-208">Resumen</span><span class="sxs-lookup"><span data-stu-id="58023-208">Summary</span></span>
<span data-ttu-id="58023-209">A continuación, se incluye un proceso generalizado para cualquier aplicación que tenga una base de datos:</span><span class="sxs-lookup"><span data-stu-id="58023-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="58023-210">Instale la aplicación en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="58023-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="58023-211">Incluya configuraciones específicas del entorno (local y Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="58023-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="58023-212">Configure los entornos de ensayo y de producción para Web Apps.</span><span class="sxs-lookup"><span data-stu-id="58023-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="58023-213">Si ya está ejecutando una aplicación de producción en Azure, sincronice el contenido de producción (archivos y código + base de datos) con el entorno local y el de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="58023-214">Desarrolle la aplicación en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="58023-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="58023-215">Coloque la aplicación web de producción en modo de mantenimiento o bloqueo y sincronice el contenido de la base de datos de producción con los entornos de ensayo y de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="58023-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="58023-216">Impleméntela en el entorno de ensayo y pruébela.</span><span class="sxs-lookup"><span data-stu-id="58023-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="58023-217">Impleméntela en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="58023-218">Repita los pasos del 4 al 6.</span><span class="sxs-lookup"><span data-stu-id="58023-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="58023-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="58023-219">Umbraco</span></span>
<span data-ttu-id="58023-220">En esta sección, aprenderá cómo la solución CMS de Umbraco usa un módulo personalizado para implementar entre varios entornos DevOps.</span><span class="sxs-lookup"><span data-stu-id="58023-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="58023-221">En este ejemplo se proporciona un enfoque diferente para administrar varios entornos de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="58023-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="58023-222">El [CMS de Umbraco](http://umbraco.com/) es una solución de CMS .NET popular entre muchos desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="58023-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="58023-223">Proporciona el módulo [Courier2](http://umbraco.com/products/more-add-ons/courier-2) para implementar desde un entorno de desarrollo a entornos de ensayo y producción.</span><span class="sxs-lookup"><span data-stu-id="58023-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="58023-224">Puede crear fácilmente un entorno de desarrollo local para una aplicación web de CMS de Umbraco mediante Visual Studio o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="58023-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="58023-225">Creación de una aplicación web de Umbraco con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58023-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="58023-226">Creación de una aplicación web de Umbraco con WebMatrix</span><span class="sxs-lookup"><span data-stu-id="58023-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="58023-227">Acuérdese siempre de quitar la carpeta `install` de la aplicación y de no cargarla nunca en aplicaciones web de ensayo o producción.</span><span class="sxs-lookup"><span data-stu-id="58023-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="58023-228">En este tutorial se usa WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="58023-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="58023-229">Configuración de un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="58023-229">Set up a staging environment</span></span>
1. <span data-ttu-id="58023-230">Cree un espacio de implementación como se mencionó antes para la aplicación web de CMS de Umbraco. Se supone que ya tiene una en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="58023-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="58023-231">Si no, puede crear una desde Marketplace.</span><span class="sxs-lookup"><span data-stu-id="58023-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="58023-232">Actualice la cadena de conexión para el espacio de implementación de ensayo de modo que apunte a la nueva base de datos **umbraco-stage-db**.</span><span class="sxs-lookup"><span data-stu-id="58023-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="58023-233">La aplicación web de producción (umbracositecms-1) y la aplicación web de ensayo (umbracositecms-1-stage) *deben* apuntar a bases de datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="58023-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Actualización de la cadena de conexión para la aplicación web de ensayo con la nueva base de datos de ensayo](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="58023-235">Haga clic en **Get Publish settings** (Obtener configuración de publicación) para el espacio de implementación **stage**.</span><span class="sxs-lookup"><span data-stu-id="58023-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="58023-236">Este proceso descargará un archivo de configuración de publicación que almacena toda la información que Visual Studio o WebMatrix necesita para publicar la aplicación desde la aplicación web de desarrollo local en la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="58023-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Obtención de configuración de publicación de la aplicación web de ensayo](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="58023-238">Abra la aplicación web de desarrollo local en WebMatrix o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58023-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="58023-239">En este tutorial se usa WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="58023-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="58023-240">En primer lugar, debe importar el archivo de configuración de publicación para la aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Importación de la configuración de publicación para Umbraco mediante WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="58023-242">Revise los cambios en el cuadro de diálogo e implemente la aplicación web local en la aplicación web de Azure: *umbracositecms-1-stage*.</span><span class="sxs-lookup"><span data-stu-id="58023-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="58023-243">Al implementar archivos directamente en la aplicación web de ensayo, se omitirán los de la carpeta `~/app_data/TEMP/`, puesto que se volverán a generar la primera vez que se inicie la aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="58023-244">Además, debe omitir el archivo `~/app_data/umbraco.config`, que también se volverá a generar.</span><span class="sxs-lookup"><span data-stu-id="58023-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Revisión de los cambios de publicación en WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="58023-246">Después de publicar correctamente la aplicación web local de Umbraco en la aplicación web de ensayo, busque esta última y ejecute algunas pruebas para descartar cualquier problema.</span><span class="sxs-lookup"><span data-stu-id="58023-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="58023-247">Configuración del módulo de implementación Courier2</span><span class="sxs-lookup"><span data-stu-id="58023-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="58023-248">Con el módulo [Courier2](http://umbraco.com/products/more-add-ons/courier-2), basta con hacer clic con el botón derecho para insertar contenido, hojas de estilos y módulos de desarrollo desde una aplicación web de ensayo en una aplicación web de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="58023-249">Este proceso reduce el riesgo de que se interrumpa la aplicación web de producción cuando se implementa una actualización.</span><span class="sxs-lookup"><span data-stu-id="58023-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="58023-250">Adquiera una licencia para Courier2 para el dominio `*.azurewebsites.net` y su dominio personalizado (por ejemplo, http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="58023-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="58023-251">Después de adquirir la licencia, coloque la licencia descargada (archivo .LIC) en la carpeta `bin`.</span><span class="sxs-lookup"><span data-stu-id="58023-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Eliminación del archivo de licencia de la carpeta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="58023-253">[Descargue el paquete de Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="58023-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="58023-254">Inicie sesión en la aplicación web de ensayo (por ejemplo, http://umbracocms-site-stage.azurewebsites.net/umbraco), haga clic en el menú **Developer** (Desarrollador) y en **Packages** > **Install local package** (Paquetes > Instalar paquete local).</span><span class="sxs-lookup"><span data-stu-id="58023-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Instalador de paquetes de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="58023-256">Cargue el paquete de Courier2 mediante el instalador.</span><span class="sxs-lookup"><span data-stu-id="58023-256">Upload the Courier2 package by using the installer.</span></span>

    ![Carga de paquete del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="58023-258">Para configurar el paquete, debe actualizar el archivo courier.config en la carpeta **Config** de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="58023-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="58023-259">En `<repositories>`, especifique la dirección URL del sitio de producción y la información de usuario.</span><span class="sxs-lookup"><span data-stu-id="58023-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="58023-260">Si está usando el proveedor de pertenencia de Umbraco predeterminado, agregue el identificador del usuario de administración en la sección &lt;user&gt;.</span><span class="sxs-lookup"><span data-stu-id="58023-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="58023-261">Si está usando un proveedor de pertenencia de Umbraco personalizado, use `<login>`,`<password>` en el módulo Courier2 para conectarse al sitio de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="58023-262">Para más información, [repase la documentación del módulo Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="58023-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="58023-263">De igual forma, instale el módulo Courier2 en el sitio de producción y configúrelo para que apunte a la aplicación web de ensayo en su archivo courier.config correspondiente, tal como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="58023-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="58023-264">Haga clic en la pestaña **Courier2** en el panel de la aplicación web de CMS de Umbraco y haga clic en **Locations** (Ubicaciones).</span><span class="sxs-lookup"><span data-stu-id="58023-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="58023-265">Debería ver el nombre del repositorio tal como se mencionó en `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="58023-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="58023-266">Siga este proceso tanto en aplicaciones web de producción como de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-266">Do this process on both your production and staging web apps.</span></span>

    ![Visualización del repositorio de la aplicación web de destino](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="58023-268">Para implementar contenido desde el sitio de ensayo en el sitio de producción, vaya a **Content** (Contenido) y seleccione una página existente o cree una.</span><span class="sxs-lookup"><span data-stu-id="58023-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="58023-269">Voy a seleccionar una página existente de mi aplicación web cuyo título es **Getting Started – new** (Introducción: nuevo) y a hacer clic en **Save and Publish** (Guardar y publicar).</span><span class="sxs-lookup"><span data-stu-id="58023-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Cambio del título de la página y publicación](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="58023-271">Haga clic con el botón derecho en la página modificada para ver todas las opciones.</span><span class="sxs-lookup"><span data-stu-id="58023-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="58023-272">Haga clic en **Courier** para abrir el cuadro de diálogo **Deployment** (Implementación).</span><span class="sxs-lookup"><span data-stu-id="58023-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="58023-273">Haga clic en **Deploy** (Implementar) para iniciar la implementación.</span><span class="sxs-lookup"><span data-stu-id="58023-273">Click **Deploy** to initiate deployment.</span></span>

    ![Cuadro de diálogo de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="58023-275">Revise los cambios y haga clic en **Continue** (Continuar).</span><span class="sxs-lookup"><span data-stu-id="58023-275">Review the changes, and then click **Continue**.</span></span>

    ![Revisión de los cambios del cuadro de diálogo de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="58023-277">El registro de implementación muestra si la implementación fue correcta.</span><span class="sxs-lookup"><span data-stu-id="58023-277">The deployment log shows if the deployment was successful.</span></span>

     ![Visualización de los registros de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="58023-279">Examine la aplicación web de producción para ver si se reflejan los cambios.</span><span class="sxs-lookup"><span data-stu-id="58023-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Examen de la aplicación web de producción](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="58023-281">Para obtener más información sobre cómo usar Courier, revise la documentación.</span><span class="sxs-lookup"><span data-stu-id="58023-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="58023-282">Actualización de la versión de CMS de Umbraco</span><span class="sxs-lookup"><span data-stu-id="58023-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="58023-283">Courier no ayudará con la actualización de una versión de CMS de Umbraco a otra.</span><span class="sxs-lookup"><span data-stu-id="58023-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="58023-284">Al actualizar la versión de CMS de Umbraco, debe comprobar si hay incompatibilidades con los módulos personalizados o de asociados y las bibliotecas principales de Umbraco.</span><span class="sxs-lookup"><span data-stu-id="58023-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="58023-285">Estos son los procedimientos recomendados:</span><span class="sxs-lookup"><span data-stu-id="58023-285">Here are best practices:</span></span>

* <span data-ttu-id="58023-286">Realice siempre una copia de seguridad de su aplicación web y de la base de datos antes de actualizar.</span><span class="sxs-lookup"><span data-stu-id="58023-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="58023-287">En las aplicaciones web de Azure, puede configurar copias de seguridad automáticas de los sitios web con la característica de copia de seguridad y restaurar el sitio en caso necesario mediante la característica de restauración.</span><span class="sxs-lookup"><span data-stu-id="58023-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="58023-288">Para obtener más detalles, consulte [Realizar una copia de seguridad de la aplicación en Azure](web-sites-backup.md) y [Restaurar una aplicación en Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="58023-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="58023-289">Compruebe si los paquetes de asociados son compatibles con la versión a la que se va a actualizar.</span><span class="sxs-lookup"><span data-stu-id="58023-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="58023-290">En la página de descarga del paquete, revise la compatibilidad del proyecto con la versión de CMS de Umbraco.</span><span class="sxs-lookup"><span data-stu-id="58023-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="58023-291">Para más información sobre cómo actualizar la aplicación web localmente, [consulte las instrucciones generales de actualización](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="58023-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="58023-292">Una vez actualizado el sitio de desarrollo local, publique los cambios en la aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="58023-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="58023-293">Pruebe la aplicación.</span><span class="sxs-lookup"><span data-stu-id="58023-293">Test your application.</span></span> <span data-ttu-id="58023-294">Si está todo bien, use el botón **Swap** (Intercambiar) para cambiar el sitio de ensayo a la aplicación web de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="58023-295">Cuando usa la operación de **intercambio**, puede ver los cambios que quedarán afectados en la configuración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="58023-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="58023-296">Esta operación de **intercambio** intercambia las aplicaciones web y las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="58023-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="58023-297">Después del **intercambio**, la aplicación web de producción apuntará a la base de datos umbraco-stage-db y la aplicación web de ensayo, a la base de datos umbraco-prod-db.</span><span class="sxs-lookup"><span data-stu-id="58023-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Vista previa de intercambio para la implementación de CMS de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="58023-299">Las ventajas de intercambiar tanto la aplicación web como la base de datos son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="58023-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="58023-300">Puede revertir a la versión anterior de la aplicación web con otro **intercambio** si hay algún problema con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="58023-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="58023-301">Para realizar una actualización, debe implementar los archivos y las bases de datos desde la aplicación web de ensayo en la aplicación web y la base de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="58023-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="58023-302">Al implementar archivos y bases de datos, pueden surgir muchos problemas.</span><span class="sxs-lookup"><span data-stu-id="58023-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="58023-303">Gracias a la característica **Swap** (Intercambiar) de los espacios, se puede reducir tanto el tiempo de inactividad durante una actualización como el riesgo de que se produzcan errores al implementar cambios.</span><span class="sxs-lookup"><span data-stu-id="58023-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="58023-304">Puede llevar a cabo **pruebas A/B** con la característica [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/).</span><span class="sxs-lookup"><span data-stu-id="58023-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="58023-305">Este ejemplo demuestra la flexibilidad de la plataforma, donde puede compilar módulos personalizados parecidos al módulo Courier de Umbraco para administrar la implementación entre entornos.</span><span class="sxs-lookup"><span data-stu-id="58023-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="58023-306">Referencias</span><span class="sxs-lookup"><span data-stu-id="58023-306">References</span></span>
[<span data-ttu-id="58023-307">Agile Software Development con el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="58023-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="58023-308">Configuración de entornos de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="58023-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="58023-309">How to block web access to non-production deployment slots (Bloqueo del acceso web a ranuras de implementación que no son de producción)</span><span class="sxs-lookup"><span data-stu-id="58023-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
