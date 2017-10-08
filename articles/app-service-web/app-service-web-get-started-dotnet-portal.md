---
title: "una aplicación web de Umbraco Hola portal de Azure en cinco minutos aaaDeploy | Documentos de Microsoft"
description: "Obtenga información acerca de lo fácil que es toorun las aplicaciones web en el servicio de aplicaciones mediante la implementación de una aplicación de ASP.NET de ejemplo. Vea los resultados inmediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Implementar una aplicación web de Umbraco Hola portal de Azure en cinco minutos

Este tutorial le ayudará a implementar n [Umbraco](https://our.umbraco.org/) aplicación web demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) en minutos.

![Aplicación de Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Requisitos previos
Necesita una cuenta de Microsoft Azure. Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure. Crear una aplicación de inicio y trabajar con él para la hora de tooan--ninguna tarjeta de crédito necesario, sin compromisos.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Implementar la aplicación ASP.NET de hello
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. Abra [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).

    Este vínculo es un método abreviado tooimmediately configurar una nueva aplicación de Umbraco Hola portal de Azure.

3. En **Nombre de la aplicación**, escriba un nombre de aplicación web. Verá una marca de verificación verde en el cuadro de hello si Hola nombre es único en hello `azurewebsites.net` dominio.
   
5. En **grupo de recursos**, haga clic en **crear nuevo** toocreate un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), a continuación, asígnele un nombre.

7. Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo). Configurar hello [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) tal como se muestra:

    - En **plan de servicio de aplicaciones**, nombre de tipo hello deseado.
    - En **ubicación**, elegir una ubicación toohost el plan.
    - Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.
    - Haga clic en **Aceptar**.

    La configuración de Umbraco CMS debe parecerse Hola siguiente captura de pantalla:

    ![Configuración en curso: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. Haga clic en **SQL Database** > **Crear una base de datos nueva**. Configurar base de datos SQL de hello tal como se muestra:

    - En **Nombre**, escriba un nombre, como **myBD**.
    - Haga clic en **Plan de tarifa** y luego seleccione **F1 Free** (F1 Gratis) u otro plan que se adapta a sus necesidades y, seguidamente, haga clic en **Seleccionar**.
    - Haga clic en **Servidor de destino** > **Crear un servidor nuevo**. Configurar el servidor de base de datos de hello tal como se muestra:

        - En **Nombre del servidor**, escriba un nombre para el servidor. Verá una marca de verificación verde en el cuadro de hello si Hola nombre es único en hello `.database.windows.net` dominio.
        - En **inicio de sesión de administrador de servidor**, Hola tipo deseado de nombre de usuario de administrador.
        - En **contraseña** y **Confirmar contraseña**, contraseña de tipo hello deseada.
        - En ubicación, seleccione Hola la misma ubicación que utiliza para la aplicación web de Hola.
        - Asegúrese de que **server tooaccess de permitir que los servicios de azure** está seleccionada.
        - Haga clic en **Seleccionar**.
    
    - Haga clic en **Seleccionar**.

13. Haga clic en **configuración de aplicación Web**, especifique el nombre de usuario de base de datos de Hola y la contraseña y haga clic en **Aceptar**.

    La configuración de Umbraco CMS debe parecerse Hola siguiente captura de pantalla:

    ![Configuración finalizada: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. Haga clic en **Crear**.
    
    Ahora, Azure crea la aplicación de Umbraco según su configuración. Verá la notificación **Implementación iniciada...**

    ![La implementación finalizó correctamente: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Inicio y administración de la aplicación web de Umbraco

Cuando Azure finalice la implementación de aplicación, verá otra notificación.

![La implementación finalizó correctamente: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Haga clic en la notificación de Hola. Si se lo haya perdido, siempre puede acceso haciendo clic en campana de notificación de hello (![siguientes notificación - Umbraco primero en el servicio de aplicación de Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Ahora verá la [hoja](../azure-resource-manager/resource-group-portal.md#manage-resources) de administración de la aplicación web (*hoja*: una página del portal que se abre horizontalmente).

3. En la parte superior de Hola de página de información general de hello, haga clic en **examinar**.
   
    ![Examinar: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Ahora puede ver Hola Umbraco **bienvenida** página. Configurar una instalación de Umbraco de Hola y comenzar a jugar con él.

    ![Configuración de Umbraco: primera aplicación de Umbraco en Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Pasos siguientes
* [Implementar una aplicación de web ASP.NET tooAzure servicio de aplicación mediante Visual Studio](app-service-web-get-started-dotnet.md) -Descubra cómo toocreate una nueva aplicación web de Azure desde Visual Studio, con cualquiera de hello incluye plantillas de la aplicación.
* [Implementar el servicio de aplicaciones de código tooAzure](web-sites-deploy.md)-Obtenga información acerca de cómo toodeploy de FTP o de origen controlar repositorios.
* [Agregar funcionalidad tooyour primera web aplicación](app-service-web-get-started-2.md) -lleve su aplicación de Azure toohello siguiente nivel. Autentique los usuarios. Escálela según la demanda. Configure algunas alertas de rendimiento. Todo ello con unos cuantos clics.
