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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Uso eficaz de entornos DevOps para las aplicaciones web
Este artículo muestra cómo tooset una copia de seguridad y administrar las implementaciones de aplicaciones web cuando haya varias versiones de la aplicación en varios entornos, como desarrollo, ensayo, control de calidad (QA) y producción. Cada versión de la aplicación puede considerarse como un entorno de desarrollo para hello exhaustivos su proceso de implementación. Por ejemplo, los programadores pueden usar Hola QA entorno tootest Hola de calidad de aplicación hello antes que push Hola cambios tooproduction.
Varios entornos de desarrollo pueden ser un reto porque necesita un código tootrack, administrar los recursos (cálculo, aplicación web, base de datos, caché, etc.) e implementar código a través de entornos.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Configuración de un entorno que no es de producción (ensayo, desarrollo, control de calidad)
Después de una aplicación web de producción esté en funcionamiento, Hola siguiente paso es toocreate un entorno no productivo. toouse ranuras de implementación, asegúrese de que está ejecutando en modo de plan de hello Standard o Premium servicio de aplicaciones de Azure. Los espacios de implementación son aplicaciones web activas que tienen sus propios nombres de host. Elementos de contenido y la configuración de aplicación Web se pueden intercambiar entre dos ranuras de implementación, incluida la zona de producción de hello. Al implementar la ranura de implementación de aplicación tooa, obtendrá Hola siguientes ventajas:

- Puede validar cambios tooa web app en una ranura de implementación de ensayo antes de intercambiar aplicación hello con la ranura de producción de hello.
- Al implementar una ranura de tooa de aplicación web en primer lugar e intercambiar en producción, todas las instancias de la ranura de Hola se activa antes de que se va a intercambiar en producción. Este proceso elimina tiempos de inactividad al implementar la aplicación web. Hola redireccionamiento del tráfico es perfecto y no se anulan solicitudes debido a las operaciones de tooswap. tooautomate este flujo de trabajo completo, configurar [intercambio automático](web-sites-staged-publishing.md#configure-auto-swap) cuando no es necesaria la validación de intercambio previo.
- Después de un intercambio, ranura de Hola que tiene la aplicación web de hello previamente almacenado provisionalmente ahora tiene Hola aplicación de web de producción anterior. Si hay cambios de hello pasados a la ranura de producción de hello no según lo esperado, puede realizar Hola mismo intercambio inmediatamente tooget la opción "última configuración válida conocida" servicios de aplicación web.

tooset una ranura de implementación de almacenamiento provisional, consulte [establecer entornos de ensayo para aplicaciones web en el servicio de aplicaciones de Azure](web-sites-staged-publishing.md). Todos los entornos deberían incluir su conjunto de recursos propio. Por ejemplo, si la aplicación web utiliza una base de datos, las aplicaciones web de producción y de ensayo deben usar bases de datos diferentes. Agregue ensayo recursos del entorno de desarrollo como base de datos, almacenamiento o caché tooset su entorno de desarrollo de ensayo.

## <a name="examples-of-using-multiple-development-environments"></a>Ejemplos del uso de varios entornos de desarrollo
Cualquier proyecto debería poner en práctica la administración de código fuente con al menos dos entornos: desarrollo y producción. Si usa sistemas de administración de contenido (CMSs), los marcos de aplicaciones, etc., la aplicación hello podría no admitir este escenario sin personalización. Esta posibilidad es true para algunos entornos populares de Hola que se describen en las secciones siguientes de Hola. Una gran cantidad de preguntas que proceder toomind cuando se trabaja con CMS/marcos, como:

- ¿Cómo se desglosan contenido Hola el en entornos diferentes?
- ¿Qué archivos se pueden cambiar sin afectar a las actualizaciones de versión del marco?
- ¿Cómo se administran las configuraciones para cada entorno?
- ¿Cómo se administran las actualizaciones de versión de módulos, complementos y el marco de trabajo de hello principal?

Hay muchas tooset formas varios entornos para el proyecto. Hello en los ejemplos siguientes muestran un método para cada aplicación respectivo.

### <a name="wordpress"></a>WordPress
En esta sección, obtendrá información sobre cómo tooset un flujo de trabajo de implementación mediante el uso de espacios de WordPress. WordPress, al igual que la mayoría de las soluciones CMS, no admite varios entornos de desarrollo sin llevar a cabo personalización. característica de las aplicaciones Web de Hola de servicio de aplicaciones de Azure tiene algunas de las características que hacen que sea fácil toostore configuración fuera de su código.

1. Antes de crear un espacio de almacenamiento provisional, configure su toosupport de código de aplicación varios entornos. toosupport varios entornos de WordPress, necesita tooedit `wp-config.php` sobre el desarrollo local de aplicación web y agregar Hola siguiente código al principio de hello del archivo hello. Este proceso habilitará la aplicación toopick Hola correcta configuración basada en entorno seleccionado Hola.

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

2. Cree una carpeta bajo la raíz de aplicación web denominada `config`y agregue hello `wp-config.azure.php` y `wp-config.local.php` archivos, que representan el entorno de Azure y el entorno local, respectivamente.

3. Copie el siguiente hello en `wp-config.local.php`:

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

    Establecer las claves de seguridad de hello tal como se muestra en el código anterior Hola puede ayudar a su aplicación web tooprevent contra la piratería informática, por lo que usar valores exclusivos. Si necesita la cadena de hello toogenerate las claves de seguridad se ha mencionado en el código de hello, puede [toohello vaya automática generador](https://api.wordpress.org/secret-key/1.1/salt) toocreate nuevos pares clave/valor.

4. Copia Hola siguiente de código en `wp-config.azure.php`:

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

#### <a name="use-relative-paths"></a>Uso de rutas de acceso relativas
Una tooconfigure lo último en la aplicación de WordPress hello es rutas de acceso relativas. WordPress almacena información de dirección URL de base de datos de Hola. Este almacenamiento dificulta mover el contenido de un entorno tooanother. Se necesita la base de datos de Hola de tooupdate cada vez que se mueve desde toostage local o en entornos de tooproduction de fase. riesgo de hello tooreduce de problemas que pueden producirse con la implementación de una base de datos cada vez que se implementa en un entorno tooanother, use hello [raíz relativa vincula complemento](https://wordpress.org/plugins/root-relative-urls/), que se puede instalar mediante el Administrador de WordPress Hola panel.

Agregar Hola siguiendo las entradas tooyour `wp-config.php` archivo antes de hello `That's all, stop editing!` comentario:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Activar el complemento de Hola a través de hello `Plugins` menú en el panel del Administrador de WordPress. Guarde la configuración de vínculo permanente para la aplicación de WordPress.

#### <a name="hello-final-wp-configphp-file"></a>Hola final `wp-config.php` archivo
Las actualizaciones principales de WordPress no afectan a los archivos `wp-config.php`, `wp-config.azure.php` ni `wp-config.local.php`. Esta es una versión final de hello `wp-config.php` archivo:

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

#### <a name="set-up-a-staging-environment"></a>Configuración de un entorno de ensayo
1. Si ya tiene una aplicación web de WordPress con su suscripción de Azure, inicie sesión en toohello [portal de Azure](http://portal.azure.com), y, a continuación, vaya tooyour WordPress web app. Si no tiene una aplicación web de WordPress, puede crear uno de hello Azure Marketplace. más información, consulte toolearn [crear una aplicación web de WordPress en el servicio de aplicación de Azure](web-sites-php-web-site-gallery.md).
Haga clic en **configuración** > **ranuras de implementación** > **agregar** toocreate una ranura de implementación con el nombre de hello *fase*. Una ranura de implementación es otra aplicación web que recursos compartidos de Hola los mismos recursos que la aplicación web principal de hello que creó anteriormente.

    ![Creación de la ranura de implementación de ensayo](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Agregar otra base de datos de MySQL, digamos `wordpress-stage-db`, grupo de recursos de tooyour `wordpressapp-group`.

    ![Agregar grupo de tooresource de base de datos de MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Actualizar las cadenas de conexión de hello para la fase implementación ranura toopoint toohello nueva base de datos `wordpress-stage-db`. La aplicación web de producción, `wordpressprodapp`y de ensayo de la aplicación web, `wordpressprodapp-stage`, bases de datos debe toodifferent de punto.

#### <a name="configure-environment-specific-app-settings"></a>Configuración de valores de aplicación específicos del entorno
Los desarrolladores pueden almacenar pares de clave/valor cadena en Azure como parte de la información de configuración de hello, denominada **configuración de la aplicación**, que tiene asociados con una aplicación web. En tiempo de ejecución, las aplicaciones web automáticamente recuperan estos valores y que estén disponible toocode que se ejecuta en la aplicación web. Desde el punto de vista de la seguridad, esto resulta beneficioso, ya que la información confidencial, como las cadenas de conexión de base de datos que incluyen contraseñas, no se muestran nunca sin cifrar en un archivo como `wp-config.php`.

Este proceso, que se explica en hello en los párrafos siguientes, es útil porque incluye cambios de archivo y los cambios de base de datos de la aplicación de WordPress de hello:

* Actualización de versión de WordPress
* Agregar nuevos complementos, o bien editar o actualizar los existentes
* Agregar nuevos temas o editar o actualizar los existentes

Configure los valores de aplicación para:

* Información de base de datos
* Activar o desactivar el registro de WordPress
* Configurar la seguridad de WordPress

![Configuración de aplicaciones para la aplicación web de Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Asegúrese de que agrega Hola después de la configuración de la aplicación para la ranura de aplicación y fase de web de producción. Tenga en cuenta que la aplicación web de producción de hello y aplicación web de ensayo usan diferentes bases de datos.

1. Desactive hello **configuración ranura** casilla de verificación para todos los parámetros de configuración de hello excepto WP_ENV. Este proceso intercambiará configuración Hola para su aplicación web, el contenido del archivo y la base de datos. Si **ranura configuración** está activa, configuraciones de aplicación y la configuración de la cadena de conexión de aplicación web de hello le *no* mover a través de entornos al realizar una **intercambiar** operación. Los cambios de base de datos que estén presentes no interrumpirán la aplicación web de producción.

2. Implementar Hola desarrollo local entorno web app toohello fase web app y la base de datos mediante WebMatrix o herramientas de generación de su elección, como FTP, Git o PhpMyAdmin.

    ![Cuadro de diálogo de publicación de WebMatrix para una aplicación web de WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Examine y pruebe la aplicación web provisional. Teniendo en cuenta un escenario donde el tema de la aplicación web de hello hello es toobe actualizado, aquí es hello aplicación web de ensayo.

    ![Examen de la aplicación web de ensayo antes del intercambio de ranuras](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Si todo está correcto, haga clic en hello **intercambiar** situado en el almacenamiento provisional toomove de aplicación web de su entorno de producción de contenido toohello. En este caso, intercambia hello web app y la base de datos de Hola a través de entornos durante cada **intercambio** operación.

    ![Vista previa de los cambios de intercambio para WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Si su escenario necesita archivos de inserción de tooonly (no hay actualizaciones de base de datos), a continuación, compruebe **configuración ranura** para hello todas las bases de datos *configuración de la aplicación* y *deconfiguracióndelascadenasdeconexión*Hola **configuración de aplicación Web** hoja dentro del portal de Azure antes de realizar Hola Hola **intercambiar**. En este caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER y la configuración predeterminada de cadena de conexión no deberían aparecer en los cambios de versión preliminar cuando realice un **intercambio**. En este momento, cuando complete hello **intercambiar** operación, Hola habrá Hola aplicación web de WordPress actualiza sólo los archivos.
    >
    >

    Antes de hacer una **intercambiar**, esta es la aplicación web de hello producción WordPress.
    ![Aplicación web de producción antes del intercambio de espacios](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Después de hello **intercambiar** operación, el tema Hola se ha actualizado en la aplicación web de producción.

    ![Aplicación web de producción después del intercambio de ranuras](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Si necesita volver tooroll, pueden ir web de producción toohello **configuración de la aplicación**y haga clic en hello **intercambiar** botón tooswap hello web app y la base de datos de la ranura de producción toostaging. Recuerde que, si los cambios de base de datos se incluyen con un **intercambiar** operación y, a continuación, Hola siguiente vez que implemente tooyour almacenamiento provisional de la aplicación web, necesita toodeploy Hola cambios toohello actual base de datos para la aplicación web de ensayo. base de datos actual de Hello podría ser la base de datos de producción anterior Hola o base de datos de fase de Hola.

#### <a name="summary"></a>Resumen
A continuación, se incluye un proceso generalizado para cualquier aplicación que tenga una base de datos:

1. Instale la aplicación hello en su entorno local.
2. Incluya configuraciones específicas del entorno (local y Azure Web Apps).
3. Configure los entornos de ensayo y de producción para Web Apps.
4. Si tiene una aplicación de producción ya se ejecuta en Azure, sincronizar sus contenido (archivos y código y base de datos) entre ensayo y toolocal entornos de producción.
5. Desarrolle la aplicación en el entorno local.
6. Colocar la aplicación web de producción en mantenimiento o modo bloqueado y sincronizar el contenido de la base de datos de entornos de producción toostaging y desarrollo.
7. Implementar toohello entorno y pruebas de almacenamiento provisional.
8. Implementar el entorno de tooproduction.
9. Repita los pasos del 4 al 6.

### <a name="umbraco"></a>Umbraco
En esta sección, obtendrá información sobre cómo Hola Umbraco CMS usa un módulo personalizado toodeploy a través de varios entornos de DevOps. Este ejemplo proporciona un enfoque diferente toomanaging varios entornos de desarrollo.

El [CMS de Umbraco](http://umbraco.com/) es una solución de CMS .NET popular entre muchos desarrolladores. Proporciona hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy de módulo de entornos de desarrollo toostaging tooproduction. Puede crear fácilmente un entorno de desarrollo local para una aplicación web de CMS de Umbraco mediante Visual Studio o WebMatrix.

- [Creación de una aplicación web de Umbraco con Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Creación de una aplicación web de Umbraco con WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Recuerde siempre hello tooremove `install` carpeta en la aplicación y la carga nunca las aplicaciones web toostage o de producción. En este tutorial se usa WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Configuración de un entorno de ensayo
1. Crear una ranura de implementación tal y como se mencionó anteriormente para hello Umbraco CMS web app, suponiendo que ya tiene una aplicación web de Umbraco CMS y se ejecuta. Si no lo hace, puede crear uno de hello Marketplace.
2. Actualizar la cadena de conexión de hello de la fase implementación ranura toopoint toohello nueva **umbraco-fase-db** base de datos. La aplicación web de producción (umbraositecms-1) y la aplicación web de ensayo (umbracositecms-1-fase) *debe* punto toodifferent bases de datos.

    ![Actualización de la cadena de conexión para la aplicación web de ensayo con la nueva base de datos de ensayo](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Haga clic en **configuración de publicación obtener** de ranura de implementación de hello **fase**. Este proceso descargará un archivo de configuración de publicación que almacena toda la información de Hola que Visual Studio o WebMatrix requiere que toopublish la aplicación de toohello de aplicación web de desarrollo local de hello, aplicaciones web de Azure.

    ![Configuración de aplicación web de ensayo de hello de publicación de Get](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Abra la aplicación web de desarrollo local en WebMatrix o Visual Studio. En este tutorial se usa WebMatrix. En primer lugar, necesita tooimport Hola publicar el archivo de configuración de la aplicación web de ensayo.

    ![Importación de la configuración de publicación para Umbraco mediante WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Ver los cambios en el cuadro de diálogo de hello e implementar la aplicación de Azure web tooyour de aplicación web local, *umbracositecms-1-fase*. Al implementar archivos directamente la aplicación web de ensayo tooyour, omitirá archivos Hola `~/app_data/TEMP/` carpeta porque se volverá a estos archivos cuando es la primera aplicación web de hello fase iniciado. También debe omitir hello `~/app_data/umbraco.config` archivo, que también se volverá a generar.

    ![Revisión de los cambios de publicación en WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Después de publicar Hola Umbraco web local aplicación toohello ensayo aplicación web correctamente, busque la aplicación web de ensayo tooyour y ejecutar unos toorule pruebas los posibles problemas.

#### <a name="set-up-hello-courier2-deployment-module"></a>Configurar el módulo de implementación de hello Courier2
Con hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) módulo, basta con hacer clic toopush contenido, hojas de estilos y módulos de desarrollo de una aplicación de web producción almacenamiento provisional del tooa de aplicación web. Este proceso reduce el riesgo de Hola de que se interrumpa la aplicación web de producción cuando se implementa una actualización.
Adquirir una licencia para Courier2 para hello `*.azurewebsites.net` dominio y su dominio personalizado (digamos http://abc.com). Después de adquirir licencias de hello, lugar Hola descargado licencia (. Archivo LIC) en hello `bin` carpeta.

![Eliminación del archivo de licencia de la carpeta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Descargar paquete de hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Inicio de sesión en tooyour fase web app, digamos http://umbracocms-site-stage.azurewebsites.net/umbraco, haga clic en hello **Developer** menú y, a continuación, haga clic en **paquetes** > **instalar paquete local**.

    ![Instalador de paquetes de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Cargar paquete de hello Courier2 mediante el instalador de Hola.

    ![Carga de paquete del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. paquete de hello tooconfigure, necesita archivo tooupdate hello courier.config Hola **Config** carpeta de la aplicación web.

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

4. En `<repositories>`, escriba Hola producción sitio URL e información de usuario.
    Si usa el proveedor de pertenencia de hello predeterminado Umbraco, Agregar identificador hello para el usuario de administración de Hola Hola &lt;usuario&gt; sección.
    Si está utilizando un proveedor de pertenencia personalizado Umbraco, use `<login>`,`<password>` en el sitio de producción de hello Courier2 módulo tooconnect toohello.
    Para obtener más detalles, [revisar la documentación de hello para el módulo de hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. De forma similar, instale el módulo de Courier2 de hello en el sitio de producción y configurar aplicación web de toopoint toohello fase en su archivo courier.config correspondientes como se muestra aquí.

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

6. Haga clic en hello **Courier2** ficha Hola panel de Umbraco CMS web app y, a continuación, haga clic en **ubicaciones**. Debería ver el nombre del repositorio hello como se mencionó en `courier.config`. Siga este proceso tanto en aplicaciones web de producción como de ensayo.

    ![Visualización del repositorio de la aplicación web de destino](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. contenido toodeploy de hello ensayo sitio toohello sitio de producción, vaya demasiado**contenido**y seleccionar una página existente o cree una nueva página. Seleccionará una página de mi aplicación web donde es el título de Hola de página de hello **Introducción – nueva**y, a continuación, haga clic en **guardar y publicar**.

    ![Cambio del título de la página y publicación](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Hola contextual modifica página tooview todas las opciones de Hola. Haga clic en **Courier** tooopen hello **implementación** cuadro de diálogo. Haga clic en **implementar** tooinitiate implementación.

    ![Cuadro de diálogo de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Revisar cambios de hello y, a continuación, haga clic en **continuar**.

    ![Revisión de los cambios del cuadro de diálogo de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    registro de la implementación de Hello muestra si la implementación de hello finalizó correctamente.

     ![Visualización de los registros de implementación del módulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Examinar el toosee de aplicación web de producción si se reflejan los cambios de Hola.

     ![Examen de la aplicación web de producción](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

toolearn más información acerca de cómo toouse Courier, revisión Hola documentación.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>¿Cómo tooupgrade Hola versión Umbraco CMS
Le permitirá Courier no le ayudarán a actualizar desde una versión de Umbraco CMS tooanother. Al actualizar una versión de Umbraco CMS, debe comprobar las incompatibilidades con los módulos personalizados o los módulos de socios y hello las bibliotecas principales de Umbraco. Estos son los procedimientos recomendados:

* Realice siempre una copia de seguridad de su aplicación web y de la base de datos antes de actualizar. En las aplicaciones web en Azure, puede configurar copias de seguridad automáticas para sus sitios Web mediante el uso de la característica de copia de seguridad de Hola y restaurar el sitio si es necesario usando la característica de restauración Hola. Para obtener más información, consulte [cómo tooback seguridad de la aplicación web](web-sites-backup.md) y [cómo toorestore su aplicación web](web-sites-restore.md).
* Compruebe si son compatibles con la versión de Hola que se va a actualizar a paquetes de socios. Página de descarga del paquete de hello, revise la compatibilidad del proyecto Hola con la versión de Umbraco CMS.

Para obtener más información acerca de cómo tooupgrade su aplicación web localmente, [consulte las instrucciones de actualización general hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Una vez que se actualiza el sitio de desarrollo local, publicar Hola cambios toohello aplicación web de ensayo. Pruebe la aplicación. Si todo está correcto, use hello **intercambiar** botón tooswap la aplicación de web de producción de almacenamiento provisional sitio toohello. Cuando usas hello **intercambiar** operación, puede ver los cambios de Hola que se verán afectados en la configuración de la aplicación web. Esto **intercambiar** operación intercambia hello las aplicaciones web y bases de datos. Después de hello **intercambiar**, Hola base de datos de producción web app will punto toohello umbraco-fase-db y Hola ensayo web app will punto tooumbraco-prod-db base de datos.

![Vista previa de intercambio para la implementación de CMS de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Éstas son ventajas del intercambio de aplicación web de hello y base de datos de hello:

* Puede revertir toohello la versión anterior de la aplicación web con otra **intercambiar** si hay algún problema de aplicación.
* Para realizar una actualización, debe toodeploy archivos y bases de datos de almacenamiento provisional de aplicación web de web app toohello producción de hello y base de datos. Al implementar archivos y bases de datos, pueden surgir muchos problemas. Mediante el uso de hello **intercambiar** característica de ranuras, podemos reducir el tiempo de inactividad durante una actualización y reducir el riesgo de Hola de errores que pueden producirse al implementar los cambios.
* Puede hacer **A realizar pruebas A/b** mediante el uso de hello [pruebas en producción](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) característica.

Este ejemplo muestra Hola flexibilidad de plataforma de Hola donde se puede compilar módulos personalizados similares tooUmbraco Courier módulo toomanage implementación a través de entornos.

## <a name="references"></a>Referencias
[Agile Software Development con el Servicio de aplicaciones de Azure](app-service-agile-software-development.md)

[Configuración de entornos de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-staged-publishing.md)

[Cómo tooblock web tener acceso a las ranuras de implementación de producción toonon](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
