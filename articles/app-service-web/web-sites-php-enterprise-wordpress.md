---
title: clase aaaEnterprise WordPress en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toohost un WordPress empresariales del sitio en el servicio de aplicaciones de Azure"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>WordPress de clase empresarial en Azure
Azure App Service proporciona un entorno escalable, seguro y fácil de usar para sitios de [WordPress][wordpress] críticos y a gran escala. Microsoft sí ejecuta en sitios de clase empresarial como hello [Office] [ officeblog] y [Bing] [ bingblog] blogs. Este artículo muestra cómo toouse Hola característica aplicaciones Web de servicio de aplicaciones de Microsoft Azure tooestablish y mantener un empresariales, el sitio de WordPress en la nube que puede administrar un gran volumen de los visitantes.

## <a name="architecture-and-planning"></a>Arquitectura y planeación
Una instalación básica de WordPress solamente tiene dos requisitos:

* **Base de datos MySQL**: este requisito está disponible a través de [ClearDB en hello Azure Marketplace][cdbnstore]. Como alternativa, puede administrar su propia instalación de MySQL en Azure Virtual Machines usando [Windows] [mysqlwindows] o [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB proporciona varias configuraciones de MySQL. Cada configuración tiene diferentes características de rendimiento. Vea hello [tienda de Azure] [ cdbnstore] para obtener información sobre las ofertas que se proporcionan a través de la tienda de Azure de Hola o directamente, como se observa en hello [sitio Web de ClearDB](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 o versiones posteriores**: Azure App Service proporciona actualmente las [versiones 5.4, 5.5 y 5.6 de PHP][phpwebsite].

  > [!NOTE]
  > Se recomienda que se Hola siempre ejecución versión más reciente de PHP para que tenga las últimas revisiones de seguridad Hola.
  >
  >

### <a name="basic-deployment"></a>Implementación básica
Si utiliza solo los requisitos básicos hello, puede crear una solución básica de una región de Azure.

![Una aplicación web de Azure y una base de datos MySQL hospedadas en una sola región de Azure][basic-diagram]

Aunque esto le permitiría crear varias instancias de aplicaciones Web de hello sitio tooscale horizontalmente la aplicación, todo lo que se hospeda dentro de centros de datos de hello en una región geográfica específica. Los visitantes de fuera de esta región pueden ver los tiempos de respuesta lentos cuando usen sitio Hola. Si los centros de datos de hello en esta región dejan de funcionar, también lo hace la aplicación.

### <a name="multi-region-deployment"></a>Implementación en varias regiones
Mediante el uso de Azure [Traffic Manager][trafficmanager], puede escalar el sitio de WordPress en varias regiones geográficas y proporcionar Hola la misma dirección URL para todos los visitantes. Todos los visitantes de a través del Administrador de tráfico y son región tooa enrutado que se basa en Hola configuración de equilibrio de carga.

![Una aplicación web de Azure, hospedada en varias regiones, con alta disponibilidad de CDBR enrutador tooroute tooMySQL en regiones][multi-region-diagram]

Dentro de cada región, todavía se debería escalar el sitio de WordPress de hello en varias instancias de aplicaciones Web, pero este ajuste de escala es la región de tooa específico. Las regiones con mucho tráfico se pueden escalar de forma diferente a las de poco tráfico.

tooreplicate y enrutar el tráfico toomultiple bases de datos MySQL, puede usar [ClearDB enrutadores de alta disponibilidad (CDBRs)] [ cleardbscale] (izquierdo se muestra) o [MySQL clúster portadora grado de edición (CGI)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Implementación en varias regiones con almacenamiento multimedia y almacenamiento en caché
Si el sitio de hello acepta cargas o archivos multimedia de hosts, use almacenamiento de blobs de Azure. Si necesita almacenamiento en caché, considere la posibilidad de [caché en Redis][rediscache], [Memcache en la nube](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), o uno de Hola otras ofertas de almacenamiento en caché en hello [Tienda de azure](http://azure.microsoft.com/gallery/store/).

![Una aplicación web de Azure, hospedada en varias regiones, con el enrutador de alta disponibilidad CDBR para MySQL con Managed Cache, Blob Storage y Content Delivery Network][performance-diagram]

Almacenamiento de blobs es distribuidos geográficamente en regiones de forma predeterminada, por lo que no tienes tooworry sobre replicación de archivos en todos los sitios. También puede habilitar hello Azure [red de entrega de contenido] [ cdn] para el almacenamiento de blobs, que distribuye los nodos de tooend de archivos que están más cerca de tooyour los visitantes.

### <a name="planning"></a>Planificación
#### <a name="additional-requirements"></a>Requisitos adicionales
| toodo esto... | Use esto... |
| --- | --- |
| **Cargar o almacenar archivos grandes** |[Complemento de WordPress para usar Blob Storage][storageplugin] |
| **Enviar correo electrónico** |[SendGrid] [ storesendgrid] hello y [complemento WordPress para usar SendGrid][sendgridplugin] |
| **Nombres de dominio personalizados** |[Configuración de un nombre de dominio personalizado en Azure App Service][customdomain] |
| **HTTPS** |[Habilitar HTTPS para una aplicación web en Azure App Service][httpscustomdomain] |
| **Validación previa de la producción** |[Configuración de entornos de ensayo para aplicaciones web en Azure App Service][staging] <p>Al mover una aplicación web de ensayo tooproduction, también mover la configuración de WordPress Hola. Asegúrese de que todos los valores son los requisitos de toohello actualizada para la aplicación de producción antes de mover tooproduction de aplicación Hola provisionalmente.</p> |
| **Supervisión y solución de problemas** |[Habilitación del registro de diagnóstico de aplicaciones web en Azure App Service][log] y [Supervisión de aplicaciones web en Azure App Service][monitor] |
| **Implementación de su sitio** |[Implementar una aplicación web en Azure App Service][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Disponibilidad y recuperación ante desastres
| toodo esto... | Use esto... |
| --- | --- |
| **Sitios de equilibrio de carga** o **sitios distribuidos geográficamente** |[Enrutamiento del tráfico con Azure Traffic Manager][trafficmanager] |
| **Copia de seguridad y restauración** |[Copia de seguridad de una aplicación web en Azure App Service][backup] y [Restauración de una aplicación web en Azure App Service][restore] |

#### <a name="performance"></a>Rendimiento
Se consigue un rendimiento en la nube de hello principalmente a través de almacenamiento en caché y la escalabilidad horizontal. Sin embargo, deben considerarse Hola memoria, ancho de banda y otros atributos de hospedaje de aplicaciones Web.

| toodo esto... | Use esto... |
| --- | --- |
| **Conocer las capacidades de las instancias del Servicio de aplicaciones** |[Detalles de precios, incluidas las funcionalidades de los niveles de App Service][websitepricing] |
| **Almacenar recursos en caché** |[Caché en Redis][rediscache], [Memcache en la nube](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), o uno de Hola otras ofertas de almacenamiento en caché en hello [tienda de Azure](/gallery/store/) |
| **Escalar su aplicación** |[Escalar una aplicación web en Azure App Service][websitescale] y [Enrutamiento de alta disponibilidad de ClearDB][cleardbscale]. Si elige toohost y administrar su propia instalación de MySQL, le convendrá [MySQL clúster CGI] [ cge] para la implementación escalada. |

#### <a name="migration"></a>Migración
Hay dos toomigrate métodos un tooAzure de sitio de WordPress servicio de aplicaciones existente:

* **[Exportar de WordPress][export]**: este método exporta contenido Hola de tu blog. A continuación, puede importar sitio WordPress hello tooa contenido nuevo en el servicio de aplicaciones de Azure mediante hello [complemento WordPress importador][import].

  > [!NOTE]
  > Aunque este proceso permite migrar el contenido, no migra ningún complemento, tema u otras personalizaciones. Debe volver a instalar estos componentes manualmente.
  >
  >
* **Migración manual**: [copia de seguridad del sitio] [ wordpressbackup] y [base de datos][wordpressdbbackup]y, a continuación, restaurarlo manualmente tooa web aplicación en Azure Servicio de aplicaciones y la base de datos de MySQL asociada. Este método es útil toomigrate altamente personalizada sitios porque evita tarea hello de instalar manualmente los complementos, los temas y otras personalizaciones.

## <a name="step-by-step-instructions"></a>Instrucciones paso a paso
### <a name="create-a-wordpress-site"></a>Creación de un sitio de WordPress
1. Hola de uso [Azure Marketplace] [ cdbnstore] toocreate una base de datos de MySQL del tamaño de hello identificados en hello [planeación y arquitectura](#planning) sección en la región de Hola o regiones donde se va a hospedar el sitio.
2. Siga los pasos de hello en [crear una aplicación web de WordPress en el servicio de aplicación de Azure] [ createwordpress] toocreate una aplicación web de WordPress. Al crear una aplicación web de hello, seleccione **usar una base de datos MySQL existente**y, a continuación, seleccione la base de datos de Hola que creó en el paso 1.

Si va a migrar un sitio de WordPress existente, vea [migrar un tooAzure existente de sitio de WordPress](#Migrate-an-existing-WordPress-site-to-Azure) después de crear una nueva aplicación web.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Migrar un tooAzure de sitio de WordPress existente
Como se mencionó en hello [planeación y arquitectura](#planning) sección, hay un sitio de WordPress a toomigrate de dos maneras:

* **Usar exportación e importación** para los sitios que no tienen mucho personalización o donde solo desea que toomove Hola contenido.
* **Use backup y restore** para los sitios que tienen una gran cantidad de personalización que desee eliminar toomove todo.

Utilice uno de hello siguientes secciones toomigrate su sitio.

#### <a name="hello-export-and-import-method"></a>Hola exportar e importar (método)
1. Use [exportar WordPress] [ export] tooexport de sus sitios.
2. Crear una aplicación web mediante los pasos de Hola Hola [crear un sitio de WordPress](#Create-a-new-WordPress-site) sección.
3. Inicie sesión en el sitio de WordPress tooyour en hello [portal de Azure][mgmtportal]y, a continuación, haga clic en **complementos** > **Agregar nuevo**. Buscar e instalar hello **importador de WordPress** complemento.
4. Después de instalar el complemento WordPress importador hello, haga clic en **herramientas** > **importación**y, a continuación, haga clic en **WordPress** toouse Hola complemento WordPress importador.
5. En hello **importación WordPress** página, haga clic en **Elegir archivo**. Buscar archivo WXR hello que se exportó desde el sitio de WordPress existente y, a continuación, haga clic en **archivo de carga e importación**.
6. Haga clic en **Enviar**. Se le pedirá que la importación de hello fue correcta.
7. Después de completar todos estos pasos, reinicie el sitio desde su **servicios de aplicaciones** hoja en hello [portal de Azure][mgmtportal].

Después de importar el sitio de hello, tendrá que hello tooperform después de la configuración de tooenable de pasos que no está en el archivo de importación de hello.

| Si usaba esto... | Haga esto... |
| --- | --- |
| **Vínculos permanentes** |En el panel de WordPress Hola de nuevo sitio de hello, haga clic en **configuración** > **permanentes**y, a continuación, actualizar la estructura de vínculos permanentes de Hola. |
| **Vínculos de imagen y multimedia** |tooupdate vínculos toohello nueva ubicación, utilice hello [terciopelo Blues actualizar las direcciones URL complemento][velvet], una búsqueda y reemplazo de herramientas, o actualice manualmente los vínculos de hello en la base de datos. |
| **Temas** |Vaya demasiado**apariencia** > **tema**y, a continuación, actualice el tema del sitio de hello según sea necesario. |
| **Menús** |Si el tema es compatible con los menús, página principal de vínculos tooyour todavía puede tener subdirectorio antiguo Hola incrustada en ellos. Vaya demasiado**apariencia** > **menús**y, a continuación, actualizarlos. |

#### <a name="hello-backup-and-restore-method"></a>Hola de copia de seguridad y restauración (método)
1. Copia de seguridad de su WordPress existente de sitio mediante el uso de información de hello en [copias de seguridad de WordPress][wordpressbackup].
2. Copia de seguridad la base de datos existente mediante el uso de información de hello en [copia de seguridad de la base de datos][wordpressdbbackup].
3. Crear una base de datos y restaurar la copia de seguridad de Hola.

   1. Adquirir una nueva base de datos de hello [Azure Marketplace][cdbnstore], o configurar una base de datos MySQL en un [Windows] [ mysqlwindows] o [Linux ] [ mysqllinux] máquina virtual.
   2. Utilice un cliente de MySQL como [MySQL Workbench] [ workbench] tooconnect toohello nuevos de base de datos e importar la base de datos de WordPress.
   3. Hola base de datos toochange Hola dominio entradas tooyour nuevo servicio de aplicaciones de Azure dominio de actualización, por ejemplo, mywordpress.azurewebsites.net. Hola de uso [buscar y reemplazar para secuencia de comandos de las bases de datos de WordPress] [ searchandreplace] toosafely cambie todas las instancias.
4. Crear una aplicación web en el portal de Azure de Hola y publicar la copia de seguridad de hello WordPress.

   1. toocreate una aplicación web que tiene una base de datos en hello [portal de Azure][mgmtportal], haga clic en **New** > **Web y móvil**  >  **Azure Marketplace** > **aplicaciones Web** > **Web app + SQL** (o **Web app + MySQL**) > **Crear**. Configurar toocreate de configuración de todos los Hola requiere una aplicación web vacía.
   2. En la copia de seguridad de WordPress, busque hello **wp-config.php** de archivo y ábralo en un editor. Reemplace Hola siguiendo las entradas con información de hello para la nueva base de datos de MySQL:

      * **Db_name**: nombre de usuario de Hola de base de datos de Hola.
      * **DB_USER**: tooaccess de usa el nombre de usuario de Hola Hola base de datos.
      * **DB_PASSWORD**: contraseña de usuario de Hola.

        Después de cambiar estas entradas, guarde y cierre hello **wp-config.php** archivo.
   3. Hola de uso [implementar una aplicación web en el servicio de aplicación de Azure] [ deploy] método de implementación de Hola de información tooenable que desee toouse y, a continuación, implementará su aplicación WordPress tooyour copia de seguridad de servicio de aplicaciones de Azure.
5. Una vez implementado el sitio de WordPress hello, debe ser nuevo sitio de tooaccess capaz de hello (como una aplicación de servicio de aplicaciones web) mediante el uso de Hola *. azurewebsite.net dirección URL del sitio de Hola.

### <a name="configure-your-site"></a>Configuración del sitio
Después de que se ha creado o migrar de sitio de WordPress hello, usar hello tras la ejecución de tooimprove de información o habilitar la funcionalidad adicional.

| toodo esto... | Use esto... |
| --- | --- |
| **Establecer el tamaño y el modo del plan de Servicio de aplicaciones y habilitar el escalado** |[Escalado de una aplicación web en Azure App Service][websitescale]. |
| **Habilitar conexiones de base de datos persistentes** |De forma predeterminada, WordPress no utiliza las conexiones de base de datos persistente, lo que podrían producir el toobecome de base de datos de conexión toohello limitado después de varias conexiones. las conexiones persistentes tooenable, instalar hello [conexiones persistentes adaptador complemento](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Mejorar el rendimiento** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Deshabilitar la cookie ARR hello</a>, que puede mejorar el rendimiento cuando se ejecuta WordPress en varias instancias de aplicaciones Web.</p></li><li><p>Activación del almacenamiento en caché. Puede usar <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">caché en Redis</a> (vista previa) con hello <a href="https://wordpress.org/plugins/redis-object-cache/">complemento WordPress para objeto caché en Redis</a>, o bien puede usar uno de hello otras ofertas de almacenamiento en caché de hello <a href="/gallery/store/">tienda de Azure</a>.</p></li><li><p>[Agilizar WordPress con Wincache](https://wordpress.org/plugins/w3-total-cache/). Wincache está habilitado de forma predeterminada para aplicaciones web. Cuando se usa conjuntamente WinCache y memoria caché dinámica, desactivar la memoria caché de archivos de WinCache, pero dejar usuario hello y caché de sesión habilitado. tooturn desactivar la memoria caché de archivos, en un archivo .ini de nivel de sistema, establezca Hola siguiente valor:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Escalar una aplicación web en Azure App Service][websitescale] y usar <a href="http://www.cleardb.com/developers/cdbr/introduction">Enrutamiento de alta disponibilidad ClearDB</a> o <a href="http://www.mysql.com/products/cluster/">MySQL Cluster CGE</a>.</p></li></ul> |
| **Usar blobs para almacenamiento** |<ol><li><p>[Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Obtenga información acerca de cómo demasiado[Hola Use red de distribución de contenido](../cdn/cdn-create-new-endpoint.md) toogeo-distribuir los datos almacenados en blobs.</p></li><li><p>Instalar y configurar hello <a href="https://wordpress.org/plugins/windows-azure-storage/">el almacenamiento de Azure para el complemento WordPress</a>.</p><p>Para detallada sobre la instalación y la información de configuración para el complemento de hello, vea hello <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">Guía de usuario</a>.</p> </li></ol> |
| **Habilitar correo electrónico** |Habilitar <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> mediante Hola almacén de Azure. Instalar hello <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid complemento</a> de WordPress. |
| **Configuración de un nombre de dominio personalizado** |[Configuración de un nombre de dominio personalizado en Azure App Service][customdomain]. |
| **Habilitar HTTPS para un nombre de dominio personalizado** |[Habilitar HTTPS para una aplicación web en Azure App Service][httpscustomdomain]. |
| **Equilibrio de carga o distribución geográfica para el sitio** |[Enrutamiento del tráfico con Azure Traffic Manager][trafficmanager]. Si usas un dominio personalizado, consulte [configurar un nombre de dominio personalizado en el servicio de aplicación de Azure] [ customdomain] para obtener información acerca de cómo toouse Traffic Manager con nombres de dominio personalizado. |
| **Activación de las copias de seguridad automatizadas** |[Copia de seguridad de una aplicación web en Azure App Service][backup]. |
| **Activación del registro de diagnósticos** |[Habilitación del registro de diagnóstico para aplicaciones web en Azure App Service][log]. |

## <a name="next-steps"></a>Pasos siguientes
* [Optimización de WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Convertir toomultisite de WordPress en el servicio de aplicación de Azure](web-sites-php-convert-wordpress-multisite.md)
* [Asistente para actualización de ClearDB para Azure](http://www.cleardb.com/store/azure/upgrade)
* [Hospedaje de WordPress en una subcarpeta de la aplicación web en Servicio de aplicaciones de Azure](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Paso a paso: Creación de un sitio de WordPress mediante Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Hospedaje de un blog existente de WordPress en Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Habilitación de vínculos permanentes descriptivos en WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [¿Cómo toomigrate y ejecute el blog de WordPress en servicio de aplicaciones de Azure](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Cómo toorun WordPress en servicio de aplicaciones de Azure para liberar](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress en Azure en menos de dos minutos](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Mover un tooAzure de blog de WordPress - parte 1: crear un blog de WordPress en Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Mover un tooAzure de blog de WordPress - parte 2: transferir el contenido](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Mover un tooAzure de blog de WordPress - parte 3: configurar su dominio personalizado](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Mover un tooAzure de blog de WordPress - parte 4: queda permanentes y las reglas de reescritura de direcciones URL](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Mover un tooAzure de blog de WordPress - parte 5: pasar de una raíz de toohello subcarpeta](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Cómo tooset seguridad un WordPress web app en su cuenta de Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Sustentación de WordPress en Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Sugerencias para WordPress en Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
>
>

## <a name="whats-changed"></a>Lo que ha cambiado
Para que un cambio de toohello Guía de tooApp servicio de sitios Web, consulte [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
