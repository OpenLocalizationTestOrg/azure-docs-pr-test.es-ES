---
title: "entornos de DevOps aaaUse eficazmente para su aplicación web | Documentos de Microsoft"
description: "Obtenga información acerca de cómo espacios de implementación de toouse tooset seguridad y administrar varios entornos de desarrollo para la aplicación"
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
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="31105-103">Uso eficaz de entornos DevOps para las aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="31105-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="31105-104">Este artículo muestra cómo tooset una copia de seguridad y administrar las implementaciones de aplicaciones web cuando haya varias versiones de la aplicación en varios entornos, como desarrollo, ensayo, control de calidad (QA) y producción.</span><span class="sxs-lookup"><span data-stu-id="31105-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="31105-105">Cada versión de la aplicación puede considerarse como un entorno de desarrollo para hello exhaustivos su proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="31105-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="31105-106">Por ejemplo, los programadores pueden usar Hola QA entorno tootest Hola de calidad de aplicación hello antes que push Hola cambios tooproduction.</span><span class="sxs-lookup"><span data-stu-id="31105-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="31105-107">Varios entornos de desarrollo pueden ser un reto porque necesita un código tootrack, administrar los recursos (cálculo, aplicación web, base de datos, caché, etc.) e implementar código a través de entornos.</span><span class="sxs-lookup"><span data-stu-id="31105-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="31105-108">Configuración de un entorno que no es de producción (ensayo, desarrollo, control de calidad)</span><span class="sxs-lookup"><span data-stu-id="31105-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="31105-109">Después de una aplicación web de producción esté en funcionamiento, Hola siguiente paso es toocreate un entorno no productivo.</span><span class="sxs-lookup"><span data-stu-id="31105-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="31105-110">toouse ranuras de implementación, asegúrese de que está ejecutando en modo de plan de hello Standard o Premium servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="31105-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="31105-111">Los espacios de implementación son aplicaciones web activas que tienen sus propios nombres de host.</span><span class="sxs-lookup"><span data-stu-id="31105-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="31105-112">Elementos de contenido y la configuración de aplicación Web se pueden intercambiar entre dos ranuras de implementación, incluida la zona de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="31105-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="31105-113">Al implementar la ranura de implementación de aplicación tooa, obtendrá Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="31105-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="31105-114">Puede validar cambios tooa web app en una ranura de implementación de ensayo antes de intercambiar aplicación hello con la ranura de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="31105-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="31105-115">Al implementar una ranura de tooa de aplicación web en primer lugar e intercambiar en producción, todas las instancias de la ranura de Hola se activa antes de que se va a intercambiar en producción.</span><span class="sxs-lookup"><span data-stu-id="31105-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="31105-116">Este proceso elimina tiempos de inactividad al implementar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31105-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="31105-117">Hola redireccionamiento del tráfico es perfecto y no se anulan solicitudes debido a las operaciones de tooswap.</span><span class="sxs-lookup"><span data-stu-id="31105-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="31105-118">tooautomate este flujo de trabajo completo, configurar [intercambio automático](web-sites-staged-publishing.md#configure-auto-swap) cuando no es necesaria la validación de intercambio previo.</span><span class="sxs-lookup"><span data-stu-id="31105-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="31105-119">Después de un intercambio, ranura de Hola que tiene la aplicación web de hello previamente almacenado provisionalmente ahora tiene Hola aplicación de web de producción anterior.</span><span class="sxs-lookup"><span data-stu-id="31105-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="31105-120">Si hay cambios de hello pasados a la ranura de producción de hello no según lo esperado, puede realizar Hola mismo intercambio inmediatamente tooget la opción "última configuración válida conocida" servicios de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31105-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="31105-121">tooset una ranura de implementación de almacenamiento provisional, consulte [establecer entornos de ensayo para aplicaciones web en el servicio de aplicaciones de Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="31105-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="31105-122">Todos los entornos deberían incluir su conjunto de recursos propio.</span><span class="sxs-lookup"><span data-stu-id="31105-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="31105-123">Por ejemplo, si la aplicación web utiliza una base de datos, las aplicaciones web de producción y de ensayo deben usar bases de datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="31105-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="31105-124">Agregue ensayo recursos del entorno de desarrollo como base de datos, almacenamiento o caché tooset su entorno de desarrollo de ensayo.</span><span class="sxs-lookup"><span data-stu-id="31105-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="31105-125">Ejemplos del uso de varios entornos de desarrollo</span><span class="sxs-lookup"><span data-stu-id="31105-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="31105-126">Cualquier proyecto debería poner en práctica la administración de código fuente con al menos dos entornos: desarrollo y producción.</span><span class="sxs-lookup"><span data-stu-id="31105-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="31105-127">Si usa sistemas de administración de contenido (CMSs), los marcos de aplicaciones, etc., la aplicación hello podría no admitir este escenario sin personalización.</span><span class="sxs-lookup"><span data-stu-id="31105-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="31105-128">Esta posibilidad es true para algunos entornos populares de Hola que se describen en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="31105-129">Una gran cantidad de preguntas que proceder toomind cuando se trabaja con CMS/marcos, como:</span><span class="sxs-lookup"><span data-stu-id="31105-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="31105-130">¿Cómo se desglosan contenido Hola el en entornos diferentes?</span><span class="sxs-lookup"><span data-stu-id="31105-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="31105-131">¿Qué archivos se pueden cambiar sin afectar a las actualizaciones de versión del marco?</span><span class="sxs-lookup"><span data-stu-id="31105-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="31105-132">¿Cómo se administran las configuraciones para cada entorno?</span><span class="sxs-lookup"><span data-stu-id="31105-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="31105-133">¿Cómo se administran las actualizaciones de versión de módulos, complementos y el marco de trabajo de hello principal?</span><span class="sxs-lookup"><span data-stu-id="31105-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="31105-134">Hay muchas tooset formas varios entornos para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="31105-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="31105-135">Hello en los ejemplos siguientes muestran un método para cada aplicación respectivo.</span><span class="sxs-lookup"><span data-stu-id="31105-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="31105-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="31105-136">WordPress</span></span>
<span data-ttu-id="31105-137">En esta sección, obtendrá información sobre cómo tooset un flujo de trabajo de implementación mediante el uso de espacios de WordPress.</span><span class="sxs-lookup"><span data-stu-id="31105-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="31105-138">WordPress, al igual que la mayoría de las soluciones CMS, no admite varios entornos de desarrollo sin llevar a cabo personalización.</span><span class="sxs-lookup"><span data-stu-id="31105-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="31105-139">característica de las aplicaciones Web de Hola de servicio de aplicaciones de Azure tiene algunas de las características que hacen que sea fácil toostore configuración fuera de su código.</span><span class="sxs-lookup"><span data-stu-id="31105-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="31105-140">Antes de crear un espacio de almacenamiento provisional, configure su toosupport de código de aplicación varios entornos.</span><span class="sxs-lookup"><span data-stu-id="31105-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="31105-141">toosupport varios entornos de WordPress, necesita tooedit `wp-config.php` sobre el desarrollo local de aplicación web y agregar Hola siguiente código al principio de hello del archivo hello.</span><span class="sxs-lookup"><span data-stu-id="31105-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="31105-142">Este proceso habilitará la aplicación toopick Hola correcta configuración basada en entorno seleccionado Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

    ```
    // Support multiple environments
    // set hello config file based on current environment
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
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="31105-143">Cree una carpeta bajo la raíz de aplicación web denominada `config`y agregue hello `wp-config.azure.php` y `wp-config.local.php` archivos, que representan el entorno de Azure y el entorno local, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="31105-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="31105-144">Copie el siguiente hello en `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="31105-144">Copy hello following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
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

    <span data-ttu-id="31105-145">Establecer las claves de seguridad de hello tal como se muestra en el código anterior Hola puede ayudar a su aplicación web tooprevent contra la piratería informática, por lo que usar valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="31105-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="31105-146">Si necesita la cadena de hello toogenerate las claves de seguridad se ha mencionado en el código de hello, puede [toohello vaya automática generador](https://api.wordpress.org/secret-key/1.1/salt) toocreate nuevos pares clave/valor.</span><span class="sxs-lookup"><span data-stu-id="31105-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="31105-147">Copia Hola siguiente de código en `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="31105-147">Copy hello following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

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
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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

#### <a name="use-relative-paths"></a><span data-ttu-id="31105-148">Uso de rutas de acceso relativas</span><span class="sxs-lookup"><span data-stu-id="31105-148">Use relative paths</span></span>
<span data-ttu-id="31105-149">Una tooconfigure lo último en la aplicación de WordPress hello es rutas de acceso relativas.</span><span class="sxs-lookup"><span data-stu-id="31105-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="31105-150">WordPress almacena información de dirección URL de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="31105-151">Este almacenamiento dificulta mover el contenido de un entorno tooanother.</span><span class="sxs-lookup"><span data-stu-id="31105-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="31105-152">Se necesita la base de datos de Hola de tooupdate cada vez que se mueve desde toostage local o en entornos de tooproduction de fase.</span><span class="sxs-lookup"><span data-stu-id="31105-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="31105-153">riesgo de hello tooreduce de problemas que pueden producirse con la implementación de una base de datos cada vez que se implementa en un entorno tooanother, use hello [raíz relativa vincula complemento](https://wordpress.org/plugins/root-relative-urls/), que se puede instalar mediante el Administrador de WordPress Hola panel.</span><span class="sxs-lookup"><span data-stu-id="31105-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="31105-154">Agregar Hola siguiendo las entradas tooyour `wp-config.php` archivo antes de hello `That's all, stop editing!` comentario:</span><span class="sxs-lookup"><span data-stu-id="31105-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="31105-155">Activar el complemento de Hola a través de hello `Plugins` menú en el panel del Administrador de WordPress.</span><span class="sxs-lookup"><span data-stu-id="31105-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="31105-156">Guarde la configuración de vínculo permanente para la aplicación de WordPress.</span><span class="sxs-lookup"><span data-stu-id="31105-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="31105-157">Hola final `wp-config.php` archivo</span><span class="sxs-lookup"><span data-stu-id="31105-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="31105-158">Las actualizaciones principales de WordPress no afectan a los archivos `wp-config.php`, `wp-config.azure.php` ni `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="31105-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="31105-159">Esta es una versión final de hello `wp-config.php` archivo:</span><span class="sxs-lookup"><span data-stu-id="31105-159">Here's a final version of hello `wp-config.php` file:</span></span>

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="31105-160">Configuración de un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="31105-160">Set up a staging environment</span></span>
1. <span data-ttu-id="31105-161">Si ya tiene una aplicación web de WordPress con su suscripción de Azure, inicie sesión en toohello [portal de Azure](http://portal.azure.com), y, a continuación, vaya tooyour WordPress web app.</span><span class="sxs-lookup"><span data-stu-id="31105-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="31105-162">Si no tiene una aplicación web de WordPress, puede crear uno de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="31105-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="31105-163">más información, consulte toolearn [crear una aplicación web de WordPress en el servicio de aplicación de Azure](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="31105-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="31105-164">Haga clic en **configuración** > **ranuras de implementación** > **agregar** toocreate una ranura de implementación con el nombre de hello *fase*.</span><span class="sxs-lookup"><span data-stu-id="31105-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="31105-165">Una ranura de implementación es otra aplicación web que recursos compartidos de Hola los mismos recursos que la aplicación web principal de hello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="31105-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Creación de la ranura de implementación de ensayo](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="31105-167">Agregar otra base de datos de MySQL, digamos `wordpress-stage-db`, grupo de recursos de tooyour `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="31105-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![Agregar grupo de tooresource de base de datos de MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="31105-169">Actualizar las cadenas de conexión de hello para la fase implementación ranura toopoint toohello nueva base de datos `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="31105-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="31105-170">La aplicación web de producción, `wordpressprodapp`y de ensayo de la aplicación web, `wordpressprodapp-stage`, bases de datos debe toodifferent de punto.</span><span class="sxs-lookup"><span data-stu-id="31105-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="31105-171">Configuración de valores de aplicación específicos del entorno</span><span class="sxs-lookup"><span data-stu-id="31105-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="31105-172">Los desarrolladores pueden almacenar pares de clave/valor cadena en Azure como parte de la información de configuración de hello, denominada **configuración de la aplicación**, que tiene asociados con una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31105-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="31105-173">En tiempo de ejecución, las aplicaciones web automáticamente recuperan estos valores y que estén disponible toocode que se ejecuta en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31105-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="31105-174">Desde el punto de vista de la seguridad, esto resulta beneficioso, ya que la información confidencial, como las cadenas de conexión de base de datos que incluyen contraseñas, no se muestran nunca sin cifrar en un archivo como `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="31105-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="31105-175">Este proceso, que se explica en hello en los párrafos siguientes, es útil porque incluye cambios de archivo y los cambios de base de datos de la aplicación de WordPress de hello:</span><span class="sxs-lookup"><span data-stu-id="31105-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="31105-176">Actualización de versión de WordPress</span><span class="sxs-lookup"><span data-stu-id="31105-176">WordPress version upgrade</span></span>
* <span data-ttu-id="31105-177">Agregar nuevos complementos, o bien editar o actualizar los existentes</span><span class="sxs-lookup"><span data-stu-id="31105-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="31105-178">Agregar nuevos temas o editar o actualizar los existentes</span><span class="sxs-lookup"><span data-stu-id="31105-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="31105-179">Configure los valores de aplicación para:</span><span class="sxs-lookup"><span data-stu-id="31105-179">Configure app settings for:</span></span>

* <span data-ttu-id="31105-180">Información de base de datos</span><span class="sxs-lookup"><span data-stu-id="31105-180">Database information</span></span>
* <span data-ttu-id="31105-181">Activar o desactivar el registro de WordPress</span><span class="sxs-lookup"><span data-stu-id="31105-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="31105-182">Configurar la seguridad de WordPress</span><span class="sxs-lookup"><span data-stu-id="31105-182">WordPress security settings</span></span>

![Configuración de aplicaciones para la aplicación web de Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="31105-184">Asegúrese de que agrega Hola después de la configuración de la aplicación para la ranura de aplicación y fase de web de producción.</span><span class="sxs-lookup"><span data-stu-id="31105-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="31105-185">Tenga en cuenta que la aplicación web de producción de hello y aplicación web de ensayo usan diferentes bases de datos.</span><span class="sxs-lookup"><span data-stu-id="31105-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="31105-186">Desactive hello **configuración ranura** casilla de verificación para todos los parámetros de configuración de hello excepto WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="31105-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="31105-187">Este proceso intercambiará configuración Hola para su aplicación web, el contenido del archivo y la base de datos.</span><span class="sxs-lookup"><span data-stu-id="31105-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="31105-188">Si **ranura configuración** está activa, configuraciones de aplicación y la configuración de la cadena de conexión de aplicación web de hello le *no* mover a través de entornos al realizar una **intercambiar** operación.</span><span class="sxs-lookup"><span data-stu-id="31105-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="31105-189">Los cambios de base de datos que estén presentes no interrumpirán la aplicación web de producción.</span><span class="sxs-lookup"><span data-stu-id="31105-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="31105-190">Implementar Hola desarrollo local entorno web app toohello fase web app y la base de datos mediante WebMatrix o herramientas de generación de su elección, como FTP, Git o PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="31105-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Cuadro de diálogo de publicación de WebMatrix para una aplicación web de WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="31105-192">Examine y pruebe la aplicación web provisional.</span><span class="sxs-lookup"><span data-stu-id="31105-192">Browse and test your staging web app.</span></span> <span data-ttu-id="31105-193">Teniendo en cuenta un escenario donde el tema de la aplicación web de hello hello es toobe actualizado, aquí es hello aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="31105-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Examen de la aplicación web de ensayo antes del intercambio de ranuras](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="31105-195">Si todo está correcto, haga clic en hello **intercambiar** situado en el almacenamiento provisional toomove de aplicación web de su entorno de producción de contenido toohello.</span><span class="sxs-lookup"><span data-stu-id="31105-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="31105-196">En este caso, intercambia hello web app y la base de datos de Hola a través de entornos durante cada **intercambio** operación.</span><span class="sxs-lookup"><span data-stu-id="31105-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Vista previa de los cambios de intercambio para WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="31105-198">Si su escenario necesita archivos de inserción de tooonly (no hay actualizaciones de base de datos), a continuación, compruebe **configuración ranura** para hello todas las bases de datos *configuración de la aplicación* y *deconfiguracióndelascadenasdeconexión*Hola **configuración de aplicación Web** hoja dentro del portal de Azure antes de realizar Hola Hola **intercambiar**.</span><span class="sxs-lookup"><span data-stu-id="31105-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="31105-199">En este caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER y la configuración predeterminada de cadena de conexión no deberían aparecer en los cambios de versión preliminar cuando realice un **intercambio**.</span><span class="sxs-lookup"><span data-stu-id="31105-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="31105-200">En este momento, cuando complete hello **intercambiar** operación, Hola habrá Hola aplicación web de WordPress actualiza sólo los archivos.</span><span class="sxs-lookup"><span data-stu-id="31105-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="31105-201">Antes de hacer una **intercambiar**, esta es la aplicación web de hello producción WordPress.</span><span class="sxs-lookup"><span data-stu-id="31105-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="31105-202">![Aplicación web de producción antes del intercambio de espacios](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="31105-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="31105-203">Después de hello **intercambiar** operación, el tema Hola se ha actualizado en la aplicación web de producción.</span><span class="sxs-lookup"><span data-stu-id="31105-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Aplicación web de producción después del intercambio de ranuras](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="31105-205">Si necesita volver tooroll, pueden ir web de producción toohello **configuración de la aplicación**y haga clic en hello **intercambiar** botón tooswap hello web app y la base de datos de la ranura de producción toostaging.</span><span class="sxs-lookup"><span data-stu-id="31105-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="31105-206">Recuerde que, si los cambios de base de datos se incluyen con un **intercambiar** operación y, a continuación, Hola siguiente vez que implemente tooyour almacenamiento provisional de la aplicación web, necesita toodeploy Hola cambios toohello actual base de datos para la aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="31105-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="31105-207">base de datos actual de Hello podría ser la base de datos de producción anterior Hola o base de datos de fase de Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="31105-208">Resumen</span><span class="sxs-lookup"><span data-stu-id="31105-208">Summary</span></span>
<span data-ttu-id="31105-209">A continuación, se incluye un proceso generalizado para cualquier aplicación que tenga una base de datos:</span><span class="sxs-lookup"><span data-stu-id="31105-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="31105-210">Instale la aplicación hello en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="31105-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="31105-211">Incluya configuraciones específicas del entorno (local y Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="31105-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="31105-212">Configure los entornos de ensayo y de producción para Web Apps.</span><span class="sxs-lookup"><span data-stu-id="31105-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="31105-213">Si tiene una aplicación de producción ya se ejecuta en Azure, sincronizar sus contenido (archivos y código y base de datos) entre ensayo y toolocal entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="31105-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="31105-214">Desarrolle la aplicación en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="31105-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="31105-215">Colocar la aplicación web de producción en mantenimiento o modo bloqueado y sincronizar el contenido de la base de datos de entornos de producción toostaging y desarrollo.</span><span class="sxs-lookup"><span data-stu-id="31105-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="31105-216">Implementar toohello entorno y pruebas de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="31105-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="31105-217">Implementar el entorno de tooproduction.</span><span class="sxs-lookup"><span data-stu-id="31105-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="31105-218">Repita los pasos del 4 al 6.</span><span class="sxs-lookup"><span data-stu-id="31105-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="31105-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="31105-219">Umbraco</span></span>
<span data-ttu-id="31105-220">En esta sección, obtendrá información sobre cómo Hola Umbraco CMS usa un módulo personalizado toodeploy a través de varios entornos de DevOps.</span><span class="sxs-lookup"><span data-stu-id="31105-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="31105-221">Este ejemplo proporciona un enfoque diferente toomanaging varios entornos de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="31105-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="31105-222">El [CMS de Umbraco](http://umbraco.com/) es una solución de CMS .NET popular entre muchos desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="31105-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="31105-223">Proporciona hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy de módulo de entornos de desarrollo toostaging tooproduction.</span><span class="sxs-lookup"><span data-stu-id="31105-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="31105-224">Puede crear fácilmente un entorno de desarrollo local para una aplicación web de CMS de Umbraco mediante Visual Studio o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="31105-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="31105-225">Creación de una aplicación web de Umbraco con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31105-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="31105-226">Creación de una aplicación web de Umbraco con WebMatrix</span><span class="sxs-lookup"><span data-stu-id="31105-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="31105-227">Recuerde siempre hello tooremove `install` carpeta en la aplicación y la carga nunca las aplicaciones web toostage o de producción.</span><span class="sxs-lookup"><span data-stu-id="31105-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="31105-228">En este tutorial se usa WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="31105-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="31105-229">Configuración de un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="31105-229">Set up a staging environment</span></span>
1. <span data-ttu-id="31105-230">Crear una ranura de implementación tal y como se mencionó anteriormente para hello Umbraco CMS web app, suponiendo que ya tiene una aplicación web de Umbraco CMS y se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="31105-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="31105-231">Si no lo hace, puede crear uno de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="31105-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="31105-232">Actualizar la cadena de conexión de hello de la fase implementación ranura toopoint toohello nueva **umbraco-fase-db** base de datos.</span><span class="sxs-lookup"><span data-stu-id="31105-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="31105-233">La aplicación web de producción (umbraositecms-1) y la aplicación web de ensayo (umbracositecms-1-fase) *debe* punto toodifferent bases de datos.</span><span class="sxs-lookup"><span data-stu-id="31105-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Actualización de la cadena de conexión para la aplicación web de ensayo con la nueva base de datos de ensayo](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="31105-235">Haga clic en **configuración de publicación obtener** de ranura de implementación de hello **fase**.</span><span class="sxs-lookup"><span data-stu-id="31105-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="31105-236">Este proceso descargará un archivo de configuración de publicación que almacena toda la información de Hola que Visual Studio o WebMatrix requiere que toopublish la aplicación de toohello de aplicación web de desarrollo local de hello, aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="31105-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Configuración de aplicación web de ensayo de hello de publicación de Get](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="31105-238">Abra la aplicación web de desarrollo local en WebMatrix o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31105-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="31105-239">En este tutorial se usa WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="31105-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="31105-240">En primer lugar, necesita tooimport Hola publicar el archivo de configuración de la aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="31105-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Importación de la configuración de publicación para Umbraco mediante WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="31105-242">Ver los cambios en el cuadro de diálogo de hello e implementar la aplicación de Azure web tooyour de aplicación web local, *umbracositecms-1-fase*.</span><span class="sxs-lookup"><span data-stu-id="31105-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="31105-243">Al implementar archivos directamente la aplicación web de ensayo tooyour, omitirá archivos Hola `~/app_data/TEMP/` carpeta porque se volverá a estos archivos cuando es la primera aplicación web de hello fase iniciado.</span><span class="sxs-lookup"><span data-stu-id="31105-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="31105-244">También debe omitir hello `~/app_data/umbraco.config` archivo, que también se volverá a generar.</span><span class="sxs-lookup"><span data-stu-id="31105-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Revisión de los cambios de publicación en WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="31105-246">Después de publicar Hola Umbraco web local aplicación toohello ensayo aplicación web correctamente, busque la aplicación web de ensayo tooyour y ejecutar unos toorule pruebas los posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="31105-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="31105-247">Configurar el módulo de implementación de hello Courier2</span><span class="sxs-lookup"><span data-stu-id="31105-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="31105-248">Con hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) módulo, basta con hacer clic toopush contenido, hojas de estilos y módulos de desarrollo de una aplicación de web producción almacenamiento provisional del tooa de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31105-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="31105-249">Este proceso reduce el riesgo de Hola de que se interrumpa la aplicación web de producción cuando se implementa una actualización.</span><span class="sxs-lookup"><span data-stu-id="31105-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="31105-250">Adquirir una licencia para Courier2 para hello `*.azurewebsites.net` dominio y su dominio personalizado (digamos http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="31105-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="31105-251">Después de adquirir licencias de hello, lugar Hola descargado licencia (. Archivo LIC) en hello `bin` carpeta.</span><span class="sxs-lookup"><span data-stu-id="31105-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Eliminación del archivo de licencia de la carpeta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="31105-253">[Descargar paquete de hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="31105-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="31105-254">Inicio de sesión en tooyour fase web app, digamos http://umbracocms-site-stage.azurewebsites.net/umbraco, haga clic en hello **Developer** menú y, a continuación, haga clic en **paquetes** > **instalar paquete local**.</span><span class="sxs-lookup"><span data-stu-id="31105-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Instalador de paquetes de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="31105-256">Cargar paquete de hello Courier2 mediante el instalador de Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Carga de paquete del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="31105-258">paquete de hello tooconfigure, necesita archivo tooupdate hello courier.config Hola **Config** carpeta de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31105-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="31105-259">En `<repositories>`, escriba Hola producción sitio URL e información de usuario.</span><span class="sxs-lookup"><span data-stu-id="31105-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="31105-260">Si usa el proveedor de pertenencia de hello predeterminado Umbraco, Agregar identificador hello para el usuario de administración de Hola Hola &lt;usuario&gt; sección.</span><span class="sxs-lookup"><span data-stu-id="31105-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="31105-261">Si está utilizando un proveedor de pertenencia personalizado Umbraco, use `<login>`,`<password>` en el sitio de producción de hello Courier2 módulo tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="31105-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="31105-262">Para obtener más detalles, [revisar la documentación de hello para el módulo de hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="31105-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="31105-263">De forma similar, instale el módulo de Courier2 de hello en el sitio de producción y configurar aplicación web de toopoint toohello fase en su archivo courier.config correspondientes como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="31105-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="31105-264">Haga clic en hello **Courier2** ficha Hola panel de Umbraco CMS web app y, a continuación, haga clic en **ubicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31105-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="31105-265">Debería ver el nombre del repositorio hello como se mencionó en `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="31105-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="31105-266">Siga este proceso tanto en aplicaciones web de producción como de ensayo.</span><span class="sxs-lookup"><span data-stu-id="31105-266">Do this process on both your production and staging web apps.</span></span>

    ![Visualización del repositorio de la aplicación web de destino](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="31105-268">contenido toodeploy de hello ensayo sitio toohello sitio de producción, vaya demasiado**contenido**y seleccionar una página existente o cree una nueva página.</span><span class="sxs-lookup"><span data-stu-id="31105-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="31105-269">Seleccionará una página de mi aplicación web donde es el título de Hola de página de hello **Introducción – nueva**y, a continuación, haga clic en **guardar y publicar**.</span><span class="sxs-lookup"><span data-stu-id="31105-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Cambio del título de la página y publicación](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="31105-271">Hola contextual modifica página tooview todas las opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="31105-272">Haga clic en **Courier** tooopen hello **implementación** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31105-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="31105-273">Haga clic en **implementar** tooinitiate implementación.</span><span class="sxs-lookup"><span data-stu-id="31105-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Cuadro de diálogo de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="31105-275">Revisar cambios de hello y, a continuación, haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="31105-275">Review hello changes, and then click **Continue**.</span></span>

    ![Revisión de los cambios del cuadro de diálogo de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="31105-277">registro de la implementación de Hello muestra si la implementación de hello finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="31105-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Visualización de los registros de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="31105-279">Examinar el toosee de aplicación web de producción si se reflejan los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Examen de la aplicación web de producción](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="31105-281">toolearn más información acerca de cómo toouse Courier, revisión Hola documentación.</span><span class="sxs-lookup"><span data-stu-id="31105-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="31105-282">¿Cómo tooupgrade Hola versión Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="31105-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="31105-283">Le permitirá Courier no le ayudarán a actualizar desde una versión de Umbraco CMS tooanother.</span><span class="sxs-lookup"><span data-stu-id="31105-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="31105-284">Al actualizar una versión de Umbraco CMS, debe comprobar las incompatibilidades con los módulos personalizados o los módulos de socios y hello las bibliotecas principales de Umbraco.</span><span class="sxs-lookup"><span data-stu-id="31105-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="31105-285">Estos son los procedimientos recomendados:</span><span class="sxs-lookup"><span data-stu-id="31105-285">Here are best practices:</span></span>

* <span data-ttu-id="31105-286">Realice siempre una copia de seguridad de su aplicación web y de la base de datos antes de actualizar.</span><span class="sxs-lookup"><span data-stu-id="31105-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="31105-287">En las aplicaciones web en Azure, puede configurar copias de seguridad automáticas para sus sitios Web mediante el uso de la característica de copia de seguridad de Hola y restaurar el sitio si es necesario usando la característica de restauración Hola.</span><span class="sxs-lookup"><span data-stu-id="31105-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="31105-288">Para obtener más información, consulte [cómo tooback seguridad de la aplicación web](web-sites-backup.md) y [cómo toorestore su aplicación web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="31105-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="31105-289">Compruebe si son compatibles con la versión de Hola que se va a actualizar a paquetes de socios.</span><span class="sxs-lookup"><span data-stu-id="31105-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="31105-290">Página de descarga del paquete de hello, revise la compatibilidad del proyecto Hola con la versión de Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="31105-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="31105-291">Para obtener más información acerca de cómo tooupgrade su aplicación web localmente, [consulte las instrucciones de actualización general hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="31105-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="31105-292">Una vez que se actualiza el sitio de desarrollo local, publicar Hola cambios toohello aplicación web de ensayo.</span><span class="sxs-lookup"><span data-stu-id="31105-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="31105-293">Pruebe la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31105-293">Test your application.</span></span> <span data-ttu-id="31105-294">Si todo está correcto, use hello **intercambiar** botón tooswap la aplicación de web de producción de almacenamiento provisional sitio toohello.</span><span class="sxs-lookup"><span data-stu-id="31105-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="31105-295">Cuando usas hello **intercambiar** operación, puede ver los cambios de Hola que se verán afectados en la configuración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31105-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="31105-296">Esto **intercambiar** operación intercambia hello las aplicaciones web y bases de datos.</span><span class="sxs-lookup"><span data-stu-id="31105-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="31105-297">Después de hello **intercambiar**, Hola base de datos de producción web app will punto toohello umbraco-fase-db y Hola ensayo web app will punto tooumbraco-prod-db base de datos.</span><span class="sxs-lookup"><span data-stu-id="31105-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Vista previa de intercambio para la implementación de CMS de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="31105-299">Éstas son ventajas del intercambio de aplicación web de hello y base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="31105-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="31105-300">Puede revertir toohello la versión anterior de la aplicación web con otra **intercambiar** si hay algún problema de aplicación.</span><span class="sxs-lookup"><span data-stu-id="31105-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="31105-301">Para realizar una actualización, debe toodeploy archivos y bases de datos de almacenamiento provisional de aplicación web de web app toohello producción de hello y base de datos.</span><span class="sxs-lookup"><span data-stu-id="31105-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="31105-302">Al implementar archivos y bases de datos, pueden surgir muchos problemas.</span><span class="sxs-lookup"><span data-stu-id="31105-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="31105-303">Mediante el uso de hello **intercambiar** característica de ranuras, podemos reducir el tiempo de inactividad durante una actualización y reducir el riesgo de Hola de errores que pueden producirse al implementar los cambios.</span><span class="sxs-lookup"><span data-stu-id="31105-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="31105-304">Puede hacer **A realizar pruebas A/b** mediante el uso de hello [pruebas en producción](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) característica.</span><span class="sxs-lookup"><span data-stu-id="31105-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="31105-305">Este ejemplo muestra Hola flexibilidad de plataforma de Hola donde se puede compilar módulos personalizados similares tooUmbraco Courier módulo toomanage implementación a través de entornos.</span><span class="sxs-lookup"><span data-stu-id="31105-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="31105-306">Referencias</span><span class="sxs-lookup"><span data-stu-id="31105-306">References</span></span>
[<span data-ttu-id="31105-307">Agile Software Development con el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="31105-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="31105-308">Configuración de entornos de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="31105-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="31105-309">Cómo tooblock web tener acceso a las ranuras de implementación de producción toonon</span><span class="sxs-lookup"><span data-stu-id="31105-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
