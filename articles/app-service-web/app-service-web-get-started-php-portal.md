---
title: "una aplicación de WordPress en hello portal de Azure en cinco minutos aaaDeploy | Documentos de Microsoft"
description: "Obtenga información acerca de lo fácil que es toorun las aplicaciones web en el servicio de aplicaciones mediante la implementación de una aplicación de WordPress. Vea los resultados inmediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Implementar una aplicación de WordPress en hello portal de Azure en cinco minutos

Este tutorial muestra cómo toodeploy su primer [WordPress](https://wordpress.org/) aplicación web demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) en minutos.

![Sitio de WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Requisitos previos
Necesita una cuenta de Microsoft Azure. Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure. Crear una aplicación de inicio y trabajar con él para la hora de tooan--ninguna tarjeta de crédito necesario, sin compromisos.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Implementar la aplicación de WordPress hello
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. Abra [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    Este vínculo es un método abreviado tooimmediately configurar una nueva aplicación de WordPress en hello portal de Azure.

3. En **Nombre de la aplicación**, escriba un nombre de aplicación web. Verá una marca de verificación verde en el cuadro de hello si Hola nombre es único en hello `azurewebsites.net` dominio.
   
5. En **grupo de recursos**, haga clic en **crear nuevo** toocreate un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), a continuación, asígnele un nombre.

6. En **Proveedor de base de datos**, seleccione **CleaDB**.

7. Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo). Configurar hello [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) tal como se muestra:

    - En **plan de servicio de aplicaciones**, nombre de tipo hello deseado.
    - En **ubicación**, elegir una ubicación toohost el plan.
    - Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.
    - Haga clic en **Aceptar**.

8. Haga clic en **Base de datos** > **Create New** (Crear nueva). Configurar base de datos SQL de hello tal como se muestra:

    - En **Nombre de la base de datos**, escriba un nombre para la base de datos. 
    - En **ubicación**, elija Hola la misma ubicación que Hola plan de servicio de aplicaciones.
    - Haga clic en **Plan de tarifa** y luego seleccione **Mercury** u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.
    - Haga clic en **Condiciones legales** y luego en **Compra**.
    - Haga clic en **Aceptar**.

9. Haga clic en **Crear**.

    Ahora, Azure crea la aplicación de WordPress según su configuración. Verá la notificación **Implementación iniciada...**

    ![Implementación iniciada: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>Inicio y administración de la aplicación web de WordPress

Cuando Azure finalice la implementación de aplicación, verá otra notificación.

![La implementación finalizó correctamente: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Haga clic en la notificación de Hola. Si se lo haya perdido, siempre puede acceso haciendo clic en campana de notificación de hello (![siguientes notificación - WordPress primero en el servicio de aplicación de Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Ahora verá la [hoja](../azure-resource-manager/resource-group-portal.md#manage-resources) de administración de la aplicación web (*hoja*: una página del portal que se abre horizontalmente).

3. En la parte superior de Hola de página de información general de hello, haga clic en **examinar**.
   
    ![Examinar: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    Ahora puede ver Hola WordPress **bienvenida** página. Configurar una instalación de WordPress de Hola y comenzar a jugar con él.

    ![Configuración de WordPress: primera aplicación de WordPress en Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Pasos siguientes
* [Crear, configurar e implementar una tooAzure de aplicación web de Laravel](app-service-web-php-get-started.md) -adquirir conocimientos básicos de hello, necesita toorun cualquier aplicación web PHP en Azure, como:

    * Crear y configurar aplicaciones en Azure desde PowerShell/Bash.
    * Establecer la versión de PHP.
    * Usar un archivo de inicio que no está en el directorio de la aplicación hello raíz.
    * Habilitar la automatización de Composer.
    * Acceder a variables de entorno específico.
    * Solucionar errores comunes.

* [Implementar el servicio de aplicaciones de código tooAzure](web-sites-deploy.md)-Obtenga información acerca de cómo toodeploy de FTP o de origen controlar repositorios.
* [Agregar funcionalidad tooyour primera web aplicación](app-service-web-get-started-2.md) -lleve su aplicación de Azure toohello siguiente nivel. Autentique los usuarios. Escálela según la demanda. Configure algunas alertas de rendimiento. Todo ello con unos cuantos clics.
