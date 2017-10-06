---
title: "aaaCreate una aplicación web de WordPress en el servicio de aplicación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un nuevo Azure web app para un blog de WordPress mediante Hola Portal de Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Creación de una aplicación web de WordPress en el Servicio de aplicaciones de Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Este tutorial muestra cómo toodeploy un blog de WordPress del sitio de hello Azure Marketplace.

Cuando haya terminado con el tutorial Hola tendrá su propio sitio de blog de WordPress seguridad y ejecutan en la nube de Hola.

![Sitio de WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

Aprenderá a realizar los siguientes procedimientos:

* ¿Cómo toofind una plantilla de aplicación Hola Azure Marketplace.
* Cómo toocreate una aplicación web en la aplicación de Azure del servicio que se basa en la plantilla de Hola.
* Cómo tooconfigure configuración de servicio de aplicaciones de Azure para hello nuevo web app y la base de datos.

Hello Azure Marketplace pone a disposición una amplia gama de aplicaciones web populares desarrollado por Microsoft, compañías de terceros e iniciativas de software de código abierto. las aplicaciones web Hola se basan en una amplia gama de entornos populares, como [PHP](/develop/nodejs/) en este ejemplo WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), y [Python](/develop/python/), tooname un menor número. una aplicación web de hello Azure Marketplace Hola solo software que necesita es explorador Hola que usa para hello toocreate [Portal de Azure](https://portal.azure.com/). 

sitio de WordPress Hola que se implementa en este tutorial usa MySQL para la base de datos de Hola. Si desea que use tooinstead base de datos SQL de base de datos de hello, consulte [Nami proyecto](http://projectnami.org/). **Proyecto Nami** también está disponible a través de hello Marketplace.

> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Microsoft Azure. Si aún no la tiene, puede [activar los beneficios de suscripción a Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) o bien [registrarse para obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/). Ahí puede crear de forma inmediata una aplicación web de corta duración para iniciarse en Servicio de aplicaciones, no se requiere tarjeta de crédito y no se establece ningún compromiso.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>Selección de WordPress y configuración para el Servicio de aplicaciones de Azure
1. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com/).
2. Haga clic en **Nuevo**.
   
    ![Crear nuevo][5]
3. Busque **WordPress** y haga clic en el icono **WordPress**. Si desea toouse base de datos de SQL en lugar de MySQL, busque **Nami proyecto**.
   
    ![WordPress desde la lista][7]
4. Después de leer la descripción de Hola de aplicación de WordPress hello, haga clic en **crear**.
   
    ![Crear](./media/web-sites-php-web-site-gallery/create.png)
5. Escriba un nombre para la aplicación web de hello en hello **aplicación Web** cuadro.
   
    Este nombre debe ser único en el dominio azurewebsites.net de hello porque Hola URL de aplicación web de hello será {nombre}. azurewebsites.net. Si el nombre de hello especificado no es único, una marca de exclamación roja aparece en el cuadro de texto de Hola.
6. Si tiene más de una suscripción, elija Hola uno desea toouse. 
7. Seleccione un **Grupo de recursos** o cree uno nuevo.
   
    Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Seleccione un **Plan de servicio de aplicaciones/Ubicación** o cree uno nuevo.
   
    Para obtener más información sobre los planes del Servicio de aplicaciones, consulte [Información general sobre los planes del Servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)    
9. Haga clic en **base de datos**y, a continuación, en hello **nueva base de datos de MySQL** hoja proporcionar valores de hello necesario para configurar la base de datos de MySQL.
   
    a. Escriba un nombre nuevo o deje el nombre predeterminado de Hola.
   
    b. Deje hello **tipo de base de datos** establecido demasiado**Shared**.
   
    c. Elija Hola misma ubicación como Hola que eligió para la aplicación web de Hola.
   
    d. Elija un plan de tarifa. Para este tutorial sirve Mercurio (gratis con un mínimo de conexiones y espacio en disco).
10. Hola **nueva base de datos de MySQL** hoja, haga clic en **Aceptar**. 
11. Hola **WordPress** hoja, acepte los términos legales de hello y, a continuación, haga clic en **crear**. 
    
     ![Configuración de la aplicación web](./media/web-sites-php-web-site-gallery/configure.png)
    
     Servicio de aplicaciones de Azure crea hello web app, normalmente en menos de un minuto. Puede ver el progreso de Hola haciendo clic en un icono de campana hello en parte superior de Hola de página del portal Hola.
    
     ![Indicador de progreso](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>Inicio y administración de la aplicación web de WordPress
1. Cuando haya finalizado la creación de aplicaciones web de hello, navegue en grupo de recursos de toohello de hello Portal de Azure en el que ha creado la aplicación hello y puede ver la aplicación web de hello y base de datos de Hola.
   
    Hola recurso adicional con el icono de bombilla de hello es [Application Insights](/services/application-insights/), que proporciona servicios de supervisión de la aplicación web.
2. Hola **grupo de recursos** hoja, haga clic en línea de aplicación web de Hola.
   
    ![Configuración de la aplicación web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. En la hoja de la aplicación hello Web, haga clic en **examinar**.
   
    ![URL del sitio][browse]
4. Hola WordPress **bienvenida** página, escriba la información de configuración de hello requerida por WordPress y, a continuación, haga clic en **instalar WordPress**.
   
    ![Configuración de WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Inicie sesión con credenciales de Hola que creó en hello **bienvenida** página.  
6. Se abre la página Panel del sitio.    
   
    ![Sitio de WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Pasos siguientes
Ha visto cómo toocreate e implementar una aplicación web PHP desde la Galería de Hola. Para obtener más información acerca del uso de PHP en Azure, vea hello [Centro para desarrolladores de PHP](/develop/php/).

Para obtener más información acerca de cómo toowork con la aplicación del servicio de aplicaciones Web, vea los vínculos de hello en hello parte izquierda de la página de hello (por ventanas del explorador extensa) o al principio de Hola de página de hello (por ventanas del explorador estrechos). 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para que un cambio de toohello Guía de tooApp servicio de sitios Web, consulte [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
