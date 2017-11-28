---
title: "aaaConnect una tooRedis de aplicación de servicio de aplicaciones web a través de hello protocolo Memcache - Azure | Documentos de Microsoft"
description: "Conectar una aplicación web en el servicio de aplicación de Azure tooRedis caché mediante Protocolo Memcache de Hola"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Conectar una aplicación web en memoria caché del servicio de aplicaciones de Azure tooRedis a través de hello protocolo Memcache
En este artículo, aprenderá cómo tooconnect un WordPress web app en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) demasiado[Azure Redis Cache] [ 12] con hello [Memcache] [ 13] protocolo. Si tiene una aplicación web existente que utiliza un servidor de Memcached para almacenar en caché en memoria, puede migrar tooAzure servicio de aplicaciones y utilice Hola cookies almacenamiento en caché la solución de Microsoft Azure con poco o ningún cambio tooyour código de la aplicación. Además, puede usar las aplicaciones existentes de Memcache experiencia toocreate muy escalables y distribuidas en el servicio de aplicación de Azure con caché en Redis de Azure para la caché en memoria, durante el uso de marcos de aplicaciones populares, como. NET, PHP, Node.js, Java y Python.  

Aplicaciones de servicio de aplicaciones Web permite este escenario de aplicación con la corrección de Memcache de aplicaciones Web de hello, que es un servidor local de Memcached que actúa como un proxy de Memcache para almacenar en caché llamadas tooAzure caché en Redis. Esto permite que cualquier aplicación que se comunica mediante datos de hello Memcache protocolo toocache con caché en Redis. Esta corrección de compatibilidad de Memcache funciona en el nivel de protocolo de hello, por lo que se puede utilizar cualquier aplicación o marco de aplicación siempre y cuando se comunica mediante Protocolo Memcache de Hola.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Requisitos previos
corrección de compatibilidad de Memcache de aplicaciones Web de Hello puede utilizarse con cualquier aplicación proporcionado por el comunica mediante Protocolo Memcache de Hola. En este ejemplo concreto, la aplicación de referencia de hello es un sitio de WordPress escalable que se puede aprovisionar desde hello Azure Marketplace.

Siga los pasos de hello descritos en los siguientes artículos:

* [Aprovisionar una instancia del programa Hola a servicio de caché de Redis de Azure][0]
* [Implementación de un sitio escalable de WordPress en Azure][1]

Una vez que tenga el sitio de WordPress escalable de hello implementadas y una instancia de caché en Redis aprovisionado estará listo tooproceed con la habilitación de corrección de compatibilidad de Memcache de hello en aplicaciones de Web del servicio de aplicación de Azure.

## Habilitar la corrección de compatibilidad de hello Memcache de aplicaciones Web
En la corrección de compatibilidad de Memcache de tooconfigure de orden, debe crear tres configuraciones de aplicación. Esto puede hacerse mediante una variedad de métodos incluidos hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715), hello [portal clásico][3], hello [Cmdlets de PowerShell de Azure] [ 5] o hello [interfaz de línea de comandos de Azure][5]. Para fines de Hola de esta entrada, voy hello toouse [Portal de Azure] [ 4] configuración de la aplicación hello tooset. Hello valores siguientes se pueden recuperar de **configuración** hoja de la instancia de caché en Redis.

![Hoja de configuración de Caché en Redis de Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### Agregar la configuración de aplicación REDIS_HOST
Hola la primera configuración de aplicación que necesita toocreate es hello **REDIS\_HOST** configuración de la aplicación. Esta opción establece hello toowhich Hola corrección de compatibilidad reenvía Hola caché información sobre el destino. Hola valor necesario para la configuración de la aplicación hello REDIS_HOST puede obtenerse de hello **propiedades** hoja de la instancia de caché en Redis.

![Nombre de host de Caché en Redis de Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Clave de hello fija de hello aplicación establecer demasiado**REDIS\_HOST** y el valor de Hola de toohello de configuración de aplicación Hola **hostname** de instancia de caché en Redis Hola.

![Configuración de aplicación de Aplicaciones web REDIS_HOST](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### Agregar la configuración de aplicación REDIS_KEY
Hola segunda configuración de aplicación que necesita toocreate es hello **REDIS\_clave** configuración de la aplicación. Este valor proporciona la instancia de caché en Redis de hello autenticación token toosecurely requiere acceso Hola. Puede recuperar valor Hola necesario para la configuración de la aplicación hello REDIS_KEY de hello **las claves de acceso** hoja de instancia de caché en Redis Hola.

![Clave principal de Caché en Redis de Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Clave de hello fija de hello aplicación establecer demasiado**REDIS\_clave** y el valor de Hola de toohello de configuración de aplicación Hola **Primary Key** de instancia de caché en Redis Hola.

![Configuración de aplicación de Sitios web de Azure REDIS_KEY](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### Agregar la configuración de aplicación MEMCACHESHIM_REDIS_ENABLE
la última configuración de la aplicación de Hello es tooenable usado Hola corrección de compatibilidad de Memcache en las aplicaciones Web, que usa Hola REDIS_HOST y REDIS_KEY toohello tooconnect caché en Redis de Azure y las llamadas de caché de hello hacia delante. Clave de hello fija de hello aplicación establecer demasiado**MEMCACHESHIM\_REDIS\_habilitar** y Hola valor demasiado**true**.

![Configuración de aplicación de Aplicaciones web MEMCACHESHIM_REDIS_ENABLE](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Cuando haya terminado de agregar configuración de la aplicación hello tres (3), haga clic en **guardar**.

## Habilitar extensión de Memcache para PHP
En orden para hello toospeak de aplicación Hola protocolo Memcache, es necesario tooinstall hello Memcache extensión tooPHP--marco del lenguaje de hello para el sitio de WordPress.

### Descargar hello php_memcache extensión
Examinar demasiado[PECL][6]. En hello categoría el almacenamiento en caché, haga clic en [memcache][7]. En la columna de descargas de hello haga clic en el vínculo DLL de Hola.

![Sitio web de PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Vínculo de subproceso no seguro (NTS) x86 de hello para la versión de Hola de PHP habilitada en las aplicaciones Web de descarga. (El valor predeterminado es PHP 5.4)

![Paquete de memcache de sitio web de PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Habilitar la extensión de hello php_memcache
Después de descargar el archivo hello, descomprima y cargar hello **php\_memcache.dll** en hello **d:\\principal\\sitio\\wwwroot\\bin\\ext\\**  directory. Después de hello php_memcache.dll cargado en la aplicación web de hello, deberá tooenable Hola extensión toohello en tiempo de ejecución de PHP. Hola tooenable Memcache extensión en el Portal de Azure, abra Hola Hola **configuración de la aplicación** hoja para la aplicación web de hello, a continuación, agregue una nueva configuración de aplicación con la clave de Hola de **PHP\_extensiones** hello y valor **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Si aplicación de hello web necesita tooload varias extensiones PHP, valor de Hola de PHP_EXTENSIONS debe ser una lista delimitada por comas de los archivos de tooDLL de rutas de acceso relativas.
> 
> 

![Configuración de aplicación de Aplicaciones web de PHP_EXTENSIONS](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

Una vez que termine, haga clic en **Guardar**.

## Instalar el complemento WordPress para Memcache
> [!NOTE]
> También puede descargar hello [Memcached objeto caché complemento](https://wordpress.org/plugins/memcached/) desde WordPress.org.
> 
> 

En la página de complementos de WordPress hello, haga clic en **Agregar nuevo**.

![Página de complemento de WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

En el cuadro de búsqueda de hello, escriba **memcached** y presione **ENTRAR**.

![Agregar nuevo complemento de WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Buscar **caché de objetos de Memcached** Hola lista, a continuación, haga clic en **instalar ahora**.

![Instalar complemento de memcache de WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Habilitar Hola complemento Memcache WordPress
> [!NOTE]
> Siga las instrucciones de hello en este blog de [cómo tooenable una extensión de sitio en las aplicaciones Web] [ 8] tooinstall Visual Studio Team Services.
> 
> 

Hola `wp-config.php` , agregue Hola siguiente código encima de comentario de edición de detención Hola casi final de hello del archivo hello.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Una vez que se han pegado este código, Mónaco guardará automáticamente el documento de Hola.

Hola siguiente paso es complemento de caché de objetos de tooenable Hola. Ello arrastrando y colocando **objeto cache.php** de **wp-contenido/plugins/memcached** carpeta toohello **wp-content** carpeta tooenable Hola objeto Memcache Funcionalidad de la memoria caché.

![Busque hello memcache objeto cache.php complemento](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Ahora que hello **objeto cache.php** archivo se encuentra en hello **wp-content** carpeta, Hola ahora está habilitada la caché de objetos de Memcached.

![Habilitar el complemento de hello memcache cache.php de objeto](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Comprobar Hola caché de objetos de Memcache funciona complemento
Ahora todos de corrección de compatibilidad de hello pasos tooenable hello Memcache de aplicaciones Web están completos. Hola lo único que queda por realizar tooverify que los datos de hello es rellenar la instancia de caché en Redis.

### Habilitar la compatibilidad de puerto no SSL de hello en caché en Redis de Azure
> [!NOTE]
> En tiempo de Hola de escribir este artículo, Hola Redis CLI no admitirá la conectividad SSL, por lo tanto hello siguientes pasos son necesarios.
> 
> 

Hola Portal de Azure, examinar la instancia de caché en Redis toohello que ha creado para esta aplicación web. Una vez abierta la hoja de la memoria caché del hello, haga clic en hello **configuración** icono.

![Botón Configuración de Caché en Redis de Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Seleccione **puertos de acceso** de lista de Hola.

![Puerto de acceso de Caché en Redis de Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Haga clic en **No** en **Permitir el acceso solo mediante SSL**.

![Puerto de acceso solo SSL de Caché en Redis de Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Verá que ahora se establece el puerto no SSL de Hola. Haga clic en **Guardar**.

![Portal de acceso no SSL de Redis de Caché en Redis de Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Conectar tooAzure caché en Redis de cli de redis
> [!NOTE]
> En este paso se supone que Redis está instalado localmente en su equipo de desarrollo. [Siga estas instrucciones para instalar Redis localmente][9].
> 
> 

Abra la consola de línea de comandos de elección y tipo hello siguiente comando:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Reemplace hello  **&lt;nombre de host de caché en redis&gt;**  con el nombre de host de hello xxxxx.redis.cache.windows.net real y Hola  **&lt;principal-key-de--caché en redis&gt;**  con la clave de acceso de Hola para caché de hello, a continuación, presione **ENTRAR**. Una vez hello CLI conecte instancia de caché en Redis toohello, emitir cualquier comando de redis. En la siguiente captura de pantalla de hello, he elegido a toolist claves Hola.

![Conectar tooAzure caché en Redis de Redis CLI en Terminal](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

las claves de Hello llamada toolist Hola deben devolver un valor. Si no es así, pruebe a navegar por la aplicación web de toohello y volver a intentarlo.

## Conclusión
¡Enhorabuena! aplicación de WordPress Hello tiene ahora un tooaid de caché en memoria centralizada en aumenta el rendimiento. Recuerde que Hola corrección de compatibilidad de Memcache de aplicaciones de Web se puede utilizar con cualquier cliente Memcache independientemente del marco de aplicación o el lenguaje de programación. tooprovide comentarios o tooask preguntas acerca de la corrección de compatibilidad de Memcache de aplicaciones Web de hello, registrar demasiado[foros de MSDN] [ 10] o [Stackoverflow][11].

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
