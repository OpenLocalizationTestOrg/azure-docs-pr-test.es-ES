---
title: "aaaConvert tooMultisite de WordPress en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo tootake una aplicación web de WordPress existente se creó mediante la Galería de hello en Azure y convertir tooWordPress la funcionalidad de multisitio"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Convertir tooMultisite de WordPress en el servicio de aplicación de Azure
## <a name="overview"></a>Información general
*Por [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

En este tutorial, aprenderá cómo tootake una aplicación web de WordPress existente creado a través de la Galería de hello en Azure y convert en la funcionalidad de multisitio WordPress instalar. Además, obtendrá información sobre cómo tooassign una tooeach de dominio personalizado de hello subsitios dentro de la instalación.

Se supone que tiene una instalación existente de WordPress. Si no lo hace, siga instrucciones de hello indicadas en [crear un sitio web de WordPress desde la Galería de hello en Azure][website-from-gallery].

Convertir un WordPress existente tooMultisite de instalación de sitio único suele ser bastante simple y muchas de hello pasos iniciales que se aquí proceden directamente de hello [crear una red] [ wordpress-codex-create-a-network] página en hello [WordPress Codex](http://codex.wordpress.org).

Comencemos.

## <a name="allow-multisite"></a>Permitir multisitio
Primero debe tooenable multisitio a través de hello `wp-config.php` archivo con hello **WP\_permitir\_MULTISITIO** constante. Hay dos tooedit métodos los archivos de aplicación web: hello en primer lugar es a través de FTP y Hola segundo a través de Git. Si no está familiarizado con cómo toosetup cualquiera de estos métodos, consulte toohello tutoriales:

* [Sitio web PHP con MySQL y FTP][website-w-mysql-and-ftp-ftp-setup]
* [Sitio web PHP con MySQL y Git][website-w-mysql-and-git-git-setup]

Abra hello `wp-config.php` archivo con el editor de Hola de su elección y agregue siguiente de hello anteriormente hello `/* That's all, stop editing! Happy blogging. */` línea.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

¡Puede que el archivo hello toosave y cargarlo servidor back-toohello!

## <a name="network-setup"></a>Configuración de la red
Inicie sesión en toohello *wp-admin* área no cliente de la aplicación web y debe aparecer un nuevo elemento en hello **herramientas** menú denominado **el programa de instalación de red**. Haga clic en **el programa de instalación de red** y rellene los detalles de saludo de la red.

![Pantalla de configuración de la red][wordpress-network-setup]

Este tutorial usa hello *subdirectorios* sitio esquema porque siempre debe funcionar y se va a configurar dominios personalizados para cada subsitio más adelante en el tutorial Hola. Sin embargo, debe ser posible toosetup un subdominio instalar si asigna un dominio a través de hello [Portal de Azure](https://portal.azure.com) y comodín DNS se configuraron correctamente.

Para obtener más información sobre el subdominio vs configuraciones subdirectorio vea Hola [tipos de red multisitio] [ wordpress-codex-types-of-networks] artículo en hello WordPress Codex.

## <a name="enable-hello-network"></a>Habilitar Hola red
red de Hello ya está configurado en la base de datos de hello, pero hay un paso tooenable Hola red funcionalidad restante. Finalizar hello `wp-config.php` configuración y asegúrese de `web.config` correctamente enruta cada sitio.

Tras hacer clic en hello **instalar** botón en hello *el programa de instalación de red* página, WordPress intentará hello tooupdate `wp-config.php` y `web.config` archivos. Sin embargo, debe comprobar siempre Hola archivos tooensure Hola actualizaciones fueron correctas. Si no es así, esta pantalla presentará con actualizaciones necesarias de Hola. Editar y guardar archivos de Hola.

Después de hacer que estas actualizaciones debe toolog out y registro nuevamente en panel de administración de wp de Hola.

Ahora debería haber un menú adicionales en la barra de administración de hello con la etiqueta **Mis sitios**. Este menú permite toocontrol la nueva red a través de hello **Administrador de red** panel.

## <a name="adding-custom-domains"></a>Incorporación de dominios personalizados
Hola [asignación de dominio de WordPress MU] [ wordpress-plugin-wordpress-mu-domain-mapping] complemento lo convierte en un sitio de tooany facilísima tooadd dominios personalizados en la red. En orden para hello complemento toooperate correctamente, deberá toodo alguna configuración adicional Hola Portal así como en el registrador de dominios.

## <a name="enable-domain-mapping-toohello-web-app"></a>Habilitar aplicación de web de toohello de asignación de dominio
Hola **libre** [servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) plan de modo no permite agregar dominios personalizados tooWeb aplicaciones. Necesitará tooswitch demasiado**Shared** o **estándar** modo. toodo esto:

* Inicie sesión en toohello Portal de Azure y busque la aplicación web. 
* Haga clic en hello **escalar verticalmente** ficha **configuración**.
* En **General**, seleccione *COMPARTIDO* o *ESTÁNDAR*
* Haga clic en **Guardar**

Puede recibir un mensaje que le pide que tooverify cambio de Hola y confirmar su aplicación web ahora puede suponer un costo, dependiendo de uso y Hola otra configuración que establezca.

Tarda unos segundos tooprocess Hola nueva configuración, por lo que ahora es un buen momento toostart al configurar el dominio.

## <a name="verify-your-domain"></a>Verificación de su dominio
Para que aplicaciones Web de Azure le permita toomap un sitio de toohello de dominio, primero debe tooverify tiene dominio de hello autorización toomap Hola. toodo por lo tanto, debe agregar una nueva entrada DNS de tooyour registro CNAME.

* Inicie sesión en el Administrador de DNS del dominio tooyour
* Cree un nuevo *awverify*
* Punto de *awverify* demasiado*awverify. YOUR_DOMAIN.azurewebsites.NET*

Puede tardar algún tiempo para toogo de cambios DNS de Hola a todos los efectos que, por lo que vaya si Hola pasos no funciona inmediatamente, realice una taza de café, a continuación, vuelva e inténtelo de nuevo.

## <a name="add-hello-domain-toohello-web-app"></a>Agregar la aplicación web de hello dominio toohello
Aplicación web de tooyour devuelto a través de hello Portal de Azure, haga clic en **configuración**y, a continuación, haga clic en **los dominios personalizados y SSL**.

Cuando Hola *configuración de SSL* son muestra, verá campos Hola donde escribirá todos los dominios de Hola que deseen tooassign tooyour web app. Si un dominio no aparece aquí, no estará disponible para la asignación dentro de WordPress, independientemente de cómo DNS de dominio de hello es el programa de instalación.

![Cuadro de diálogo de administración de dominios personalizados][wordpress-manage-domains]

Después de escribir su dominio en el cuadro de texto hello, Azure comprobará Hola registro CNAME que creó anteriormente. Si no se ha propagado completamente Hola DNS, se mostrará un indicador rojo. Si fue correcto, verá una marca de verificación verde. 

Tome nota de hello que muestra la dirección IP final Hola del cuadro de diálogo de Hola. Necesitará esta hello toosetup un registro para el dominio.

## <a name="setup-hello-domain-a-record"></a>Registro de hello dominio A la instalación
Si hello otros pasos se realizaron correctamente, ahora puede asignar el dominio de aplicación web de Azure hello tooyour a través de un registro A DNS. 

Es importante toonote aquí que aplicaciones web de Azure aceptan CNAME y registros, sin embargo, *debe* usar una asignación de dominio adecuado de un registro tooenable. Un CNAME no se reenviarán tooanother CNAME, que es lo que Azure crea automáticamente con YOUR_DOMAIN.azurewebsites.net.

Utilizando la dirección IP de Hola desde el paso anterior de Hola, devolver tooyour el Administrador de DNS y el programa de instalación Hola una IP estática toothat toopoint registros.

## <a name="install-and-setup-hello-plugin"></a>Instalar y configurar el complemento de Hola
La funcionalidad de multisitio de WordPress actualmente no tiene un método integrado toomap los dominios personalizados. Sin embargo, hay un complemento llamado [asignación de dominio de WordPress MU] [ wordpress-plugin-wordpress-mu-domain-mapping] que agrega la funcionalidad de Hola para usted. Inicie sesión en la parte del Administrador de red de toohello de su sitio e instale hello **asignación de dominio de WordPress MU** complemento.

Después de instalar y activar el complemento de hello, visite **configuración** > **asignación dominio** tooconfigure Hola complemento. En el cuadro de texto de primer hello, *dirección IP del servidor*, entrada Hola dirección IP utilizada toosetup Hola un registro para el dominio de Hola. Defina cualquiera *opciones del dominio* que desee (valores predeterminados de Hola a menudo son válidos) y haga clic en **guardar**.

## <a name="map-hello-domain"></a>Asignar un dominio de Hola
Visite hello **panel** para el sitio de hello desea toomap dominio Hola. Haga clic en **herramientas** > **asignación dominio** y tipo hello nuevo dominio en el cuadro de texto de Hola y haga clic en **agregar**.

De forma predeterminada, Hola nuevo dominio será toohello ha vuelto a escribir autogenerado sitio. Si desea toohave todo el tráfico enviado toohello nuevo dominio, comprobar hello *dominio principal para este blog* cuadro antes de guardar. Puede agregar un número ilimitado de sitio de tooa de dominios, pero sólo uno puede ser principal.

## <a name="do-it-again"></a>Vuelva a hacerlo
Las aplicaciones Web de Azure le permiten tooadd un número ilimitado de aplicación web de tooa de dominios. tooadd otro dominio necesitará hello tooexecute **comprobar el dominio** y **configurar registro de dominio A hello** secciones para cada dominio.    

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


