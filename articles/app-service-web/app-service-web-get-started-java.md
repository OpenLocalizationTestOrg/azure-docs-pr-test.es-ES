---
title: "aaaCreate su primera aplicación web de Java en Azure"
description: "Obtenga información acerca de cómo toorun aplicaciones web en el servicio de aplicaciones mediante la implementación de una aplicación básica de Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Creación de su primera aplicación web de Java en Azure

Hola [aplicaciones Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) característica de [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) proporciona un servicio de hospedaje web muy escalable, aplicación de revisiones automáticamente. Este tutorial rápido muestra cómo toodeploy un Java web tooApp servicio de aplicación mediante el uso de hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).

!["Hello Azure!" aplicación web de ejemplo](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial rápido, instalar:

* Hola libre [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/). Este guía de inicio rápido utiliza Eclipse Neon.
* Hola [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Creación de un proyecto web dinámico en Eclipse

En Eclipse, seleccione **File (Archivo)** > **New (Nuevo)** > **Dynamic Web Project (Proyecto web dinámico)**.

Hola **nueva Dynamic Web Project** cuadro de diálogo, proyecto de hello name **MyFirstJavaOnAzureWebApp**y seleccione **finalizar**.
   
![Cuadro de diálogo New Dynamic Web Project (Nuevo proyecto web dinámico)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Agregar una página JSP

Si no se muestra el Explorador de proyectos, restáurelo.

![Área de trabajo de Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

En el Explorador de proyectos, expanda hello **MyFirstJavaOnAzureWebApp** proyecto.
Haga clic con el botón derecho en **WebContent** (Contenido web) y, a continuación, seleccione **New** (Nuevo) > **JSP File** (Archivo JSP).

![Menú de un nuevo archivo JSP en el Explorador de proyectos](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

Hola **New JSP File** cuadro de diálogo:

* Archivo de nombre hello **index.jsp**.
* Seleccione **Finalizar**.

  ![Cuadro de diálogo Nuevo archivo JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

En el archivo index.jsp de hello, reemplace hello `<body></body>` elemento con hello sigue marcado:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Guarde los cambios de Hola.

## <a name="publish-hello-web-app-tooazure"></a>Publicar hello web app tooAzure

En el Explorador de proyectos, haga clic en proyecto de hello y, a continuación, seleccione **Azure** > **publicar como aplicación Web de Azure**.

![Menú contextual Publish as Azure Web App (Publicar como aplicación web de Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

Hola **inicio de sesión en Azure** cuadro de diálogo, mantener hello **Interactive** opción y, a continuación, seleccione **iniciar sesión en**.

Siga instrucciones de inicio de sesión de Hola.

### <a name="deploy-web-app-dialog-box"></a>Cuadro de diálogo Implementar una aplicación web

Una vez que haya iniciado sesión tooyour cuenta de Azure, Hola **implementar aplicación de Web** aparece el cuadro de diálogo.

Seleccione **Crear**.

![Cuadro de diálogo Implementar una aplicación web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Cuadro de diálogo Crear servicio de aplicaciones

Hola **crear servicio en la aplicación** aparece el cuadro de diálogo con los valores predeterminados. Hola número **170602185241** se muestra en hello después de imagen es diferente en el cuadro de diálogo.

![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-web-get-started-java/cas1.png)

Hola **crear servicio en la aplicación** cuadro de diálogo:

* Mantenga el nombre de hello generado para la aplicación web de Hola. Este nombre debe ser único en Azure. Hola nombre forma parte de la dirección URL de hello para la aplicación web de Hola. Por ejemplo: si es el nombre de la aplicación hello **MyJavaWebApp**, Hola dirección URL es *myjavawebapp.azurewebsites.net*.
* Mantenga el contenedor de web predeterminado de Hola.
* Seleccione una suscripción de Azure.
* En hello **plan de servicio de aplicaciones** ficha:

  * **Cree una nueva**: mantener predeterminado de hello, que es el nombre de Hola de hello plan de servicio de aplicaciones.
  * **Ubicación**: seleccione **Europa occidental** o una ubicación cerca de usted.
  * **Nivel de precios**: seleccione Hola opción disponible. Para ver las características, consulte [Precios de App Service](https://azure.microsoft.com/pricing/details/app-service/).

   ![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Pestaña Grupo de recursos

Seleccione hello **grupo de recursos** ficha. Mantenga el valor de generada de manera predeterminada de Hola Hola para grupo de recursos.

![Pestaña Grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Seleccione **Crear**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Hola Kit de herramientas de Azure crea la aplicación web de hello y muestra un cuadro de diálogo de progreso.

![Cuadro de diálogo de progreso Crear App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Cuadro de diálogo Implementar una aplicación web

Hola **implementar aplicación de Web** cuadro de diálogo, seleccione **implementar tooroot**. Si tiene un servicio de aplicaciones en *wingtiptoys.azurewebsites.net* y no se implementan toohello raíz, aplicación web de hello denominado **MyFirstJavaOnAzureWebApp** se implementa demasiado *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Cuadro de diálogo Implementar una aplicación web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

cuadro de diálogo Hola Hola se muestra en Azure, JDK y las selecciones de contenedor de web.

Seleccione **implementar** toopublish hello web app tooAzure.

Cuando finalice la publicación de hello, seleccione hello **publicada** vínculo Hola **Azure Activity Log** cuadro de diálogo.

![Cuadro de diálogo Registro de actividad de Azure](./media/app-service-web-get-started-java/aal.png)

¡Enhorabuena! Ha implementado correctamente su tooAzure de aplicación web. 

!["Hello Azure!" aplicación web de ejemplo](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Actualizar la aplicación web de Hola

Cambiar Hola ejemplo código JSP tooa mensaje diferente.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Guarde los cambios de Hola.

En el Explorador de proyectos, haga clic en proyecto de hello y, a continuación, seleccione **Azure** > **publicar como aplicación Web de Azure**.

Hola **implementar aplicación de Web** aparece el cuadro de diálogo y muestra Hola servicio de aplicaciones que creó anteriormente. 

> [!NOTE]
> Seleccione **implementar tooroot** cada vez que publique.
>

Seleccione la aplicación web de hello y seleccione **implementar**, que publica los cambios de Hola.

Cuando Hola **publicación** vínculo aparece, seleccione aplicación web de toobrowse toohello y ver los cambios de Hola.

## <a name="manage-hello-web-app"></a>Administrar la aplicación web de hello

Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toosee hello web aplicación que ha creado.

En el menú izquierdo de hello, seleccione **grupos de recursos**.

![Grupos de tooresource de exploración del portal](media/app-service-web-get-started-java/rg.png)

Seleccione el grupo de recursos de Hola. página de Hello muestra los recursos de Hola que creó en este tutorial rápido.

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

Seleccione hello web app (**170602193915 webapp** Hola anterior imagen).

Hola **Introducción** aparecerá la página. Esta página proporciona una visión de cómo está haciendo la aplicación hello. En ella, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. Hola a la izquierda Hola de página Hola pestañas: Hola diferentes configuraciones que se pueden abrir. 

![Página de App Service en Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Asignación de un dominio personalizado](app-service-web-tutorial-custom-domain.md)
