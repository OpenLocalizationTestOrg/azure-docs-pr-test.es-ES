---
title: "aaaConfigure PHP en aplicaciones de Web del servicio de aplicación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure Hola instalación de PHP predeterminado o agregar una instalación de PHP personalizada para las aplicaciones Web en el servicio de aplicación de Azure."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a>Configuración de PHP en Aplicaciones web del Servicio de aplicaciones de Azure
## <a name="introduction"></a>Introducción
Esta guía le mostrará cómo tooconfigure Hola integrado en tiempo de ejecución PHP para las aplicaciones Web en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714), proporcione un tiempo de ejecución PHP personalizado y habilitar las extensiones. toouse servicio de aplicaciones, regístrese para hello [evaluación gratuita]. Hola tooget más de esta guía, primero debe crear una aplicación web PHP en el servicio de aplicaciones.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Cómo: cambiar versión PHP de integrados de Hola
PHP 5.5 está instalado de forma predeterminada y está disponible para utilizarse inmediatamente después de crear una aplicación web de App Service. Hola mejor manera toosee Hola versión disponible "revisión", su configuración predeterminada, y extensiones habilitadas hello es un script que llame hello toodeploy [phpinfo()] (función).

Las versiones de PHP 5.6 y PHP 7.0 también están disponibles, pero no están habilitadas de forma predeterminada. Hola tooupdate versión PHP, siga uno de estos métodos:

### <a name="azure-portal"></a>Portal de Azure
1. Examinar la aplicación web de tooyour en hello [Portal de Azure](https://portal.azure.com) y haga clic en hello **configuración** botón.
   
    ![Configuración de aplicaciones web][settings-button]
2. De hello **configuración** seleccione hoja **configuración de la aplicación** y elija la nueva versión PHP Hola.
   
    ![Configuración de la aplicación][application-settings]
3. Haga clic en hello **guardar** situado en la parte superior de Hola de hello **configuración de aplicación Web** hoja.
   
    ![Guardar la configuración][save-button]

### <a name="azure-powershell-windows"></a>Azure PowerShell (Windows)
1. Abra PowerShell de Azure y la cuenta de inicio de sesión tooyour:
   
        PS C:\> Login-AzureRmAccount
2. Establezca la versión de PHP de hello para la aplicación web de Hola.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. Ahora se establece la versión de PHP Hola. Puede confirmar esta configuración:
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Interfaz de línea de comandos de Azure (Linux, Mac, Windows)
toouse Hola interfaz de línea de comandos de Azure, debe tener **Node.js** instalados en su equipo.

1. Abrir Terminal y la cuenta de inicio de sesión tooyour.
   
        azure login
2. Establezca la versión de PHP de hello para la aplicación web de Hola.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. Ahora se establece la versión de PHP Hola. Puede confirmar esta configuración:
   
        azure site show {app-name}

> [!NOTE] 
> Hola [CLI de Azure 2.0](https://github.com/Azure/azure-cli) son comandos que son equivalente toohello anterior:
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Cómo: cambiar las configuraciones de PHP integradas Hola
Para cualquier tiempo de ejecución PHP integrado, puede cambiar cualquiera de las opciones de configuración de hello siguiendo estos pasos Hola. (Para obtener información acerca de las directivas, consulte la [lista de directivas de php.ini]).

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>Cambio de PHP\_INI\_USUARIO, PHP\_INI\_PERDIR, PHP\_INI\_todas LAS opciones de configuración
1. Agregar un [. user.ini] directorio raíz del archivo tooyour.
2. Agregar configuración configuración toohello `.user.ini` archivo utilizando Hola la misma sintaxis que se usan en un `php.ini` archivo. Por ejemplo, si deseara hello tooturn `display_errors` configuración y defina `upload_max_filesize` configuración too10M, su `.user.ini` archivo contendría este texto:
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Implemente la aplicación web.
4. Reinicie la aplicación web de hello. (Es necesario reiniciar debido a que lee de la frecuencia de hello con qué PHP `.user.ini` archivos se rige por hello `user_ini.cache_ttl` configuración, que es una configuración de nivel de sistema y es de 300 segundos (5 minutos) de forma predeterminada. Reiniciar aplicación web de hello fuerza las nuevas opciones de hello del tooread PHP en hello `.user.ini` archivo.)

Como una alternativa toousing una `.user.ini` archivo, puede usar hello [ini_set()] función en Opciones de configuración de tooset de secuencias de comandos que no son directivas de nivel de sistema.

### <a name="changing-phpinisystem-configuration-settings"></a>Cambiar la configuración de PHP\_INI\_SYSTEM
1. Agregar un tooyour de configuración de la aplicación Web App con la clave de hello `PHP_INI_SCAN_DIR` y valor`d:\home\site\ini`
2. Crear un `settings.ini` archivo mediante la consola de Kudu (http://&lt;nombre del sitio&gt;. scm.azurewebsite.net) en hello `d:\home\site\ini` directory.
3. Agregar configuración configuración toohello `settings.ini` archivo utilizando Hola la misma sintaxis que se usan en un archivo php.ini. Por ejemplo, si deseara hello toopoint `curl.cainfo` configuración tooa `*.crt` de archivos y establezca 'wincache.maxfilesize' establecer too512K, su `settings.ini` archivo contendría este texto:
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Reinicie los cambios de hello tooload de aplicación Web.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Cómo: habilitar extensiones en tiempo de ejecución PHP Hola predeterminado
Como se indicó en la sección anterior de hello, versión de PHP de hello mejor manera toosee Hola de forma predeterminada, su configuración predeterminada y Hola habilitado las extensiones son toodeploy un script que llame [phpinfo()]. tooenable extensiones adicionales, siga estos pasos hello:

### <a name="configure-via-ini-settings"></a>Configurar mediante configuración de ini
1. Agregar un `ext` toohello directorio `d:\home\site` directorio.
2. Colocar `.dll` archivos de extensión de hello `ext` directorio (por ejemplo, `php_xdebug.dll`). Asegúrese de que las extensiones de hello son compatibles con la versión predeterminada de PHP y son VC9 y compatible no subprocesos (nts).
3. Agregar un tooyour de configuración de la aplicación Web App con la clave de hello `PHP_INI_SCAN_DIR` y valor`d:\home\site\ini`
4. Cree un archivo `ini` en `d:\home\site\ini` denominado `extensions.ini`.
5. Agregar configuración configuración toohello `extensions.ini` archivo utilizando Hola la misma sintaxis que se usan en un archivo php.ini. Por ejemplo, si deseara tooenable Hola MongoDB y XDebug las extensiones, su `extensions.ini` archivo contendría este texto:
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Reinicie los cambios de hello tooload de aplicación Web.

### <a name="configure-via-app-setting"></a>Configurar a través de la configuración de la aplicación
1. Agregar un `bin` directorio raíz de toohello.
2. Colocar `.dll` archivos de extensión de hello `bin` directorio (por ejemplo, `php_xdebug.dll`). Asegúrese de que las extensiones de hello son compatibles con la versión predeterminada de PHP y son VC9 y compatible no subprocesos (nts).
3. Implemente la aplicación web.
4. Aplicación web de tooyour Hola Portal de Azure y haga clic en hello **configuración** botón.
   
    ![Configuración de aplicaciones web][settings-button]
5. De hello **configuración** seleccione hoja **configuración de la aplicación** y desplácese toohello **configuración de la aplicación** sección.
6. Hola **configuración de la aplicación** , debe crearse un **PHP_EXTENSIONS** clave. valor de Hola para esta clave sería una raíz de ruta de acceso relativa toowebsite: **bin\your-ext-file**.
   
    ![Habilitar extensiones en app settings][php-extensions]
7. Haga clic en hello **guardar** situado en la parte superior de Hola de hello **configuración de aplicación Web** hoja.
   
    ![Guardar la configuración][save-button]

También se pueden usar las extensiones Zend mediante una clave **PHP_ZENDEXTENSIONS**. tooenable varias extensiones, incluye una lista separada por comas de `.dll` archivos para el valor de configuración de aplicación Hola.

## <a name="how-to-use-a-custom-php-runtime"></a>Cómo: Usar un tiempo de ejecución de PHP personalizado
En lugar de hello tiempo de ejecución PHP de forma predeterminada, las aplicaciones de servicio Web de aplicación puede usar un tiempo de ejecución PHP que proporcione tooexecute scripts PHP. se puede configurar en tiempo de ejecución de Hola que proporcione un `php.ini` archivo también proporcionado. toouse un tiempo de ejecución PHP personalizada con aplicaciones Web, siga estos pasos Hola.

1. Obtenga una versión compatible con VC9 y VC11 no segura para subprocesos de PHP para Windows. Las versiones recientes de PHP para Windows se pueden encontrar aquí: [http://windows.php.net/download/]. Las versiones anteriores pueden encontrarse en el archivo de hello aquí: [http://windows.php.net/downloads/releases/archives/].
2. Modificar hello `php.ini` archivo para el tiempo de ejecución. Tenga en cuenta que Aplicaciones web omitirá cualquier configuración que se corresponda con directivas que sean solo de nivel de sistema. (Para obtener información acerca de las directivas solo a nivel de sistema, consulte la [lista de directivas de php.ini]).
3. Si lo desea, agregar en tiempo de ejecución de las extensiones tooyour PHP y habilitarlas en hello `php.ini` archivo.
4. Agregar un `bin` directorio raíz de tooyour y directorio de hello put que contiene el tiempo de ejecución PHP en él (por ejemplo, `bin\php`).
5. Implemente la aplicación web.
6. Aplicación web de tooyour Hola Portal de Azure y haga clic en hello **configuración** botón.
   
    ![Configuración de aplicaciones web][settings-button]
7. De hello **configuración** seleccione hoja **configuración de la aplicación** y desplácese toohello **asignaciones de controlador** sección. Agregar `*.php` toohello extensión campo y agregar toohello de ruta de acceso de hello `php-cgi.exe` ejecutable. Si coloca el tiempo de ejecución PHP en hello `bin` directorio en hello raíz de su aplicación, ruta de acceso de hello será `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![Especificar el controlador en hander mappings][handler-mappings]
8. Haga clic en hello **guardar** situado en la parte superior de Hola de hello **configuración de aplicación Web** hoja.
   
    ![Guardar la configuración][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Procedimiento para habilitar la automatización de Composer en Azure
De forma predeterminada, el Servicio de aplicaciones no responde con composer.json, si tiene uno en el proyecto PHP. Si usa [Git implementación](app-service-deploy-local-git.md), puede habilitar composer.json procesamiento durante `git push` habilitando la extensión de hello compositor.

> [!NOTE]
> Aquí puede [votar por soporte técnico de primera clase para Composer en el Servicio de aplicaciones](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip).
> 
> 

1. En su PHP web hoja de la aplicación Hola [portal de Azure](https://portal.azure.com), haga clic en **herramientas** > **extensiones**.
   
    ![Tooenable de hoja de configuración de Portal Azure automatización compositor en Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. Haga clic en **Agregar** y, luego, en **Compositor**.
   
    ![Agregar automatización Compositor de compositor extensión tooenable en Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. Haga clic en **Aceptar** tooaccept los términos legales. Haga clic en **Aceptar** extensión Hola de tooadd nuevo.
   
    Hola **extensiones instaladas** hoja mostrará ahora la extensión del compositor de Hola.  
    ![Acepte la automatización de Compositor de tooenable condiciones legales en Azure](./media/web-sites-php-configure/composer-extension-view.png)
4. Ahora, realizar `git add`, `git commit`, y `git push` al igual que en la sección anterior de Hola. Verá que Composer está instalando las dependencias definidas en composer.json.
   
    ![Implementación de GIT con la automatización de Composer en Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

[evaluación gratuita]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[lista de directivas de php.ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

